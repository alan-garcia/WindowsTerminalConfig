# Configuración de Windows Terminal + Oh My Posh

Esta guía explica cómo personalizar **Windows Terminal** utilizando **Oh My Posh** y una fuente compatible con iconos (Nerd Fonts) para obtener una terminal moderna y visualmente más atractiva.


## 1. Instalar Windows Terminal

Descargar [Windows Terminal](https://apps.microsoft.com/detail/9n0dx20hk701) desde Microsoft Store.


## 2. Instalar una fuente compatible con iconos

Para que los temas de **Oh My Posh** muestren correctamente iconos y glifos especiales, es necesario utilizar una fuente compatible con **Nerd Fonts**. Por ejemplo, puedes descargar **RobotoMono Nerd Font** [RobotoMono Nerd Font](https://github.com/ryanoasis/nerd-fonts/releases/download/v3.4.0/RobotoMono.zip).

Puedes consultar más fuentes compatibles en: https://www.nerdfonts.com/font-downloads.

---

Para instalar la fuente:
1. Abre **Configuración → Personalización → Fuentes**.
2. Arrastra los archivos `.ttf` descargados a la ventana de fuentes.
3. Espera a que Windows complete la instalación.

<img width="1604" height="651" alt="image" src="https://github.com/user-attachments/assets/09c04c8a-9f87-4d8f-a6b5-0faffe6a08d4" />

---

Para configurar la fuente en Windows Terminal:
1. Abre **Windows Terminal**.
2. Ve a **Configuración → Windows PowerShell → Apariencia**.
3. En la sección **Tipo de fuente**, selecciona la fuente Nerd Font instalada anteriormente.
4. Guarda los cambios.


<img width="1230" height="677" alt="image" src="https://github.com/user-attachments/assets/19d41564-1131-495a-aeb3-c1f624bc8a56" />


## 3. Instalar "Oh My Posh"

Abre Windows Terminal sobre **PowerShell**, y ejecuta el siguiente comando para instalar "Oh My Posh":

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; Invoke-Expression ((New-Object System.Net.WebClient).DownloadString('https://ohmyposh.dev/install.ps1'))
```

Para más información, ve a la documentación oficial de [Oh My Posh](https://ohmyposh.dev/docs/installation/windows).

---

Descargamos un [tema](https://ohmyposh.dev/docs/themes) de Oh My Posh. En este ejemplo, utilizaremos el tema llamado [clean-detailed](https://github.com/JanDeDobbeleer/oh-my-posh/blob/main/themes/clean-detailed.omp.json).

A continuación, descarga el archivo `.json` del tema elegido y guárdalo en una ubicación accesible para tu usuario.

Ejemplo:

```text
C:\Users\<usuario>\clean-detailed.omp.json
```

## 4. Crear el perfil de PowerShell

Un perfil de PowerShell es un script que se ejecuta automáticamente cada vez que abres una sesión de PowerShell. Su función es permitir personalizar el entorno sin tener que ejecutar manualmente los mismos comandos cada vez que abres la terminal.

Si el perfil aún no existe, fuerza a crear uno ejecutando el siguiente comando de PowerShell:

```powershell
New-Item -Path $PROFILE -Type File -Force
```

Luego, abrimos el perfil con el programa "Bloc de notas":

```powershell
notepad $PROFILE
```

Dentro de este archivo de perfil, agrega la siguiente línea:

```txt
oh-my-posh init pwsh --config ~/clean-detailed.omp.json | Invoke-Expression
```

> **Nota:** Este ejemplo asume que el archivo `clean-detailed.omp.json` se encuentra en el directorio de usuario. Si lo has guardado en otra ubicación, sustituye la ruta por la correspondiente.

Una vez guardados los cambios, cierra Windows Terminal, y vuelve a abrirlo. Si todo ha ido correctamente, el nuevo tema aparecerá aplicado automáticamente.


# Extra: Instalar iconos en PowerShell (opcional)

Para mostrar iconos según el tipo de archivo o directorio, puedes instalar en PowerShell el módulo [Terminal Icons](https://github.com/devblackops/terminal-icons).

Abre PowerShell, y ejecuta el siguiente comando:

```powershell
Install-Module -Name Terminal-Icons -Repository PSGallery
```

Abre nuevamente tu perfil de PowerShell:

```powershell
notepad $PROFILE
```

Debajo de la línea de inicialización de **Oh My Posh**, agrega la siguiente línea:

```text
Import-Module -Name Terminal-Icons
```

El contenido final del perfil de PowerShell quedaría de la siguiente manera:

```powershell
oh-my-posh init pwsh --config ~/clean-detailed.omp.json | Invoke-Expression
Import-Module -Name Terminal-Icons
```

Una vez guardados los cambios, cierra Windows Terminal, y vuelve a abrirlo.

A partir de ese momento, además de cargar automáticamente el tema de "Oh My Posh", cargará también el módulo de los iconos en cada sesión de PowerShell.
