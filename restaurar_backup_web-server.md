import glob
import os
import subprocess

def obtener_ultimo(hhh):
    archivos = glob.glob(hhh)
    if not archivos:
        return None
    return sorted(archivos)[-1]

ruta_bdd = "/home/fran/backup_project/backup_fran_db_data_*.tar.gz"
ruta_web = "/home/fran/backup_project/backup_fran_wp_data_*.tar.gz"

print("--- Selector de Backups ---")
print("1. Base de Datos (BDD)")
print("2. Código Web")

opcion = input("Elige una opción (1 o 2): ")

if opcion == "1":
    resultado = obtener_ultimo(ruta_bdd)
    tipo = "Base de Datos"
    carpeta_destino = "/var/lib/docker/volumes/fran_db_data/_data/"
elif opcion == "2":
    resultado = obtener_ultimo(ruta_web)
    tipo = "Código Web"
    carpeta_destino = "/var/lib/docker/volumes/fran_wp_data/_data/"
else:
    resultado = None
    print("Opción no válida.")

if resultado:
    print(f"\nHas elegido {tipo}.")
    print(f"El archivo más reciente es: {resultado}")

    nombre_archivo = os.path.basename(resultado)

    usuario_remoto = "fran"
    ip_remota = "192.168.10.55"
    carpeta_destino = "/home/fran/wordpress-files/"

     # Copiar archivo backup al directorio temporal remoto de Docker (para evitar problemas de permisos de escritura directa en volúmenes)
    print(f"==> Enviando {nombre_archivo} a la máquina remota...")
    subprocess.run(["rsync", "-avz", resultado, f"{usuario_remoto}@{ip_remota}:{carpeta_destino}"])

    print("\n==> ¡Proceso finalizado con éxito!")

elif opcion in ["1", "2"]:
    print(f"\nNo se encontraron archivos para {tipo}.")
