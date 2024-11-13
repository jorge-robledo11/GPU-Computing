# Documentación para la Configuración de CUDA en WSL

## Introducción

Esta guía describe los pasos seguidos para instalar CUDA Toolkit en un entorno WSL (Windows Subsystem for Linux) y asegurarse de que el compilador `nvcc` esté disponible y correctamente configurado. Esto es útil para quienes desean realizar cómputo en GPU desde Linux en WSL utilizando hardware NVIDIA.

## Requisitos Previos

- **WSL2** habilitado en Windows.
- **GPU NVIDIA** compatible con CUDA.
- **Drivers de NVIDIA actualizados** en Windows.
- **Instalación de WSL con Ubuntu** (u otra distribución compatible).

## Pasos de Configuración

### Paso 1: Verificar que la GPU esté disponible en WSL

Ejecuta el siguiente comando en la terminal de WSL para verificar que `nvidia-smi` detecta correctamente la GPU:

```bash
nvidia-smi
```

Si nvidia-smi no está disponible o no detecta la GPU, asegúrate de tener los últimos drivers de NVIDIA instalados en Windows y de estar usando WSL 2.

### Paso 2: Descargar el Instalador de CUDA para WSL
Accede al sitio de NVIDIA para descargar el instalador de CUDA específico para WSL. Puedes hacerlo utilizando wget en la terminal de WSL. Por ejemplo:

```bash
wget https://developer.download.nvidia.com/compute/cuda/12.6.0/local_installers/cuda-repo-wsl-ubuntu-12-6-local_12.6.2-1_amd64.deb
```

Nota: Asegúrate de usar la versión específica compatible con tu sistema. En este caso, estamos utilizando 12.6.2 como ejemplo.

### Paso 3: Instalar el Paquete de CUDA
Una vez descargado el paquete .deb, instálalo usando dpkg:
```bash
sudo dpkg -i cuda-repo-wsl-ubuntu-12-6-local_12.6.2-1_amd64.deb
```

### Paso 4: Añadir la Clave GPG
Después de la instalación, es posible que debas añadir la clave GPG del repositorio:
```bash
sudo cp /var/cuda-repo-wsl-ubuntu-12-6-local/cuda-clave-keyring.gpg /usr/share/keyrings/
```

### Paso 5: Actualizar el Repositorio e Instalar CUDA
Actualiza el índice de paquetes e instala CUDA:
```bash
sudo apt-get update
sudo apt-get install -y cuda
```

### Paso 6: Verificar la Instalación de nvcc
Para comprobar que nvcc (el compilador de CUDA) está instalado y disponible en tu sistema, ejecuta:
```bash
nvcc --version
```

Deberías ver información de la versión de CUDA, lo cual indica que la instalación fue exitosa.

