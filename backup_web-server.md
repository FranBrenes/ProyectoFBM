import subprocess
import datetime
import sys

# Máquina Origen
DOCKER_HOST = "192.168.10.55"
DOCKER_USER = "fran"
VOLUMENES = ["fran_db_data", "fran_wp_data"]

# Máquina Destino
DEST_HOST = "192.168.10.52"
DEST_USER = "fran"
DEST_PATH = "/home/fran/backup_projects/"

DATE_TAG = datetime.datetime.now().strftime("%Y_%m_%d_%H_%M")

def main():
    for vol in VOLUMENES:
        nombre_archivo = f"backup_{vol}_{DATE_TAG}.tar.gz"
        print(f"==> Ordenando backup de {vol} en la máquina {DOCKER_HOST}...")

        # Crear el tar.gz dentro de la máquina de origen
        cmd_comprimir_remoto = (
            f"ssh {DOCKER_USER}@{DOCKER_HOST} "
            f"\"sudo tar -czf /tmp/{nombre_archivo} -C /var/lib/docker/volumes/{vol}/_data .\""
        )

        resultado_tar = subprocess.run(cmd_comprimir_remoto, shell=True)

        # tar devuelve 0 o 1 (archivo modificado durante proceso) Ambos son válidos.
        if resultado_tar.returncode not in [0, 1]:
            sys.exit(1)

        # Mover el archivo de la Máquina Docker a la Máquina Destino
        print(f"==> Transfiriendo archivo desde la máquina Docker hacia el destino final...")
        cmd_rsync = (
            f"rsync -avz {DOCKER_USER}@{DOCKER_HOST}:/tmp/{nombre_archivo} {DEST_PATH}"
        )
        subprocess.run(cmd_rsync, shell=True, check=True)

         # Borrar el temporal en la máquina de Docker
        print(f"==> Limpiando archivos temporales en {DOCKER_HOST}...")
        cmd_limpiar = f"ssh {DOCKER_USER}@{DOCKER_HOST} 'sudo rm /tmp/{nombre_archivo}'"
        subprocess.run(cmd_limpiar, shell=True, check=True)

        print(f"Proceso completo para {vol}\n")

if __name__ == "__main__":
    main()
