# Dell-Latitude-5411-OpenCore-Big-Sur

_Herramientas:_

* Para montar la particion EFI: [MountEFI] https://github.com/corpnewt/MountEFI
* Para configurar config.plist: https://github.com/corpnewt/ProperTree
* Para Generar SMBios: https://github.com/corpnewt/GenSMBIOS

_Config Bios:_
```
Boot mode: UEFI
Fast Boot: Minimal
SecureBoot = Disable
SATA Mode: AHCI 
Intel SGX: Software Controlled
Thunderbolt Configuration: No Security
```

_Crear USB boot_
```
sudo /Applications/Install\ macOS\ Big\ Sur.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume
```

_Descargamos la carpeta EFI preconfigurada_

* [EFI.zip](https://www.mediafire.com/file/gm0kqil402qzvsg/EFI.zip/file)
* Montamos la Particion EFI del USB-BOOT y pegamos la carpeta EFI descargada

_Ejecutamos el pendrive y en el arranque seleccionamos modGRUBShell.efi (Mucho cuidado con estos comandos)_
```
CFG Lock
    (VarOffset/VarName): 0x3E
    VarStore: 0x11
    Name: CpuSetup
    
    Comando para modGRUBShell.efi: setup_var_cv CpuSetup 0x3E 0x11 0x0
____________________________________________________________________

DVMT Pre-Allocated
    (VarOffset/VarName): 0xF5
    VarStore: 0x16
    Name: SaSetup

    Comando para modGRUBShell.efi: setup_var_cv SaSetup 0xF5 0x16 0x2
____________________________________________________________________

DVMT Total Gfx Mem
    (VarOffset/VarName): 0xF6
    VarStore: 0x16
    Name: SaSetup

    Comando para modGRUBShell.efi: setup_var_cv SaSetup 0xF6 0x16 0x3
____________________________________________________________________

VT-d
    (VarOffset/VarName): 0xF9
    VarStore: 0x16
    Name: SaSetup
    
    Comando para modGRUBShell.efi: setup_var_cv SaSetup 0xF9 0x16 0x0
```

* Despues de ejecutar los comandos APAGAMOS la maquina

* Ejecutamos de nuevo el USB-BOOT e instalamos normalmente [En caso de que no inicie, ejecuta el USB-BOOT y en el menu seleciona CleanNvram o ResetNvram]

* Una vez iniciado el escritorio de Big Sur descargamos la herramienta https://github.com/corpnewt/MountEFI para montar la particion EFI del Disco Interno y del USB-BOOT

* Copiamos la carpeta EFI de USB-BOOT y la pegamos en la particion EFI del disco interno

* Desconecamos el USB-BOOT y reiniciamos asi vemos que inicie normalmente

* Recuerda generar un nuevo SMBios https://github.com/corpnewt/GenSMBIOS
```
Dentro de GenSMBios:
Seleccionamos opcion 2 y arrastamos el config.plist de la carpeta EFI del disco interno
Seleccionamos opcion 3 asi le inyecta al config.plist el GenSMBios nuevo
```

_Lo que funciona_
* Trackpad full
* HDMI
* USB-C | DP DisplayPort
* Puertos USB
* Wifi
* Conexion LAN
* Bluetooth
* Resolucion 4K

_Lo que no he probado_
* jack audio 3.5
* SDXC reader

_Reportar si hay algo que no anda tratare de repararlo_
