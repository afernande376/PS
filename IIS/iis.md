# S I N     T E R M I N A R

# UT3: Instalción y configuración de un servidor web IIS en Windows

Vamos a aprender a realizar la configuración de un servidor web IIS en Windows, pero en vez de utilizar el entorno gráfico lo realizaremos mediante comandos de Powershell. 
La instalación  configuración del rol DHCP medianet comandos Powershell se puede realizar de dos maneras:
** Localmente
** Remotamente

En esta ocuasión veremos cómo realizaralo localmente. Recuerda que antes de comenzar a trabajar, debes disponer de la misma informacion previa que necesitarías en caso de realizar la configuración de manualmente, es decir, necesitas:

* Servidor configurado con una dirección IP estática. 
* Nombre del sitio web que queresmo crear. 
* Ruta de acceso física. 
* Nombre del host (nombre DNS). 
* IP y puerto a través de la cuál se va a publicar. 


Una vez que dispongas de toda la información ya puedes proceder a seguir los pasos para instalar un servidor DHCP utilizando comandos Powershell:

1. Abre un terminal de PowerShell con permisos de administrador. 

2. Configura una dirección IP estática para el servidor:

 ```
	New-NetIPAddress -IPAddress 10.0.0.1 -InterfaceAlias "Ethernet" -DefaultGateway 10.0.0.254 -AddressFamily IPv4 -PrefixLength 24
	```
	Y añadimos el servidor DNS:

	```
Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses 10.0.1.48
	```

3. Comprobar si el rol IIS está instalado. 

	```
	Get-WindowsFeature -Name Web-Server

	```
> *También se puede ejecutar `Get-WindowsFeature`y comprobar en la lista si IIS está marcado. El nombre de búsqueda usado en el comando anterior, es el de la segunda columna de la salida del comando sin flags.* 
 
1. Si está instalado (quizás lo has instalado gráficamente), lo vamos a desinstalar. 

	```
	Uninstall-WindowsFeature -Name Web-Server

	```

5. Reiniciamos el servidor:

	```
	Restart-Computer
	```

6. Instalamos el rol IIS. Para ello debes comprobar previamente el nombre del rol. Lo puedes obtener a partir del comando observando la segunda columna:

	```
	Get-WindowsFeature 
	```
	Y ya puedes instalarlo:

	```
Install-WindowsFeature Web-Server

	```
Y compruebas que está instalado:

	```
Get-Windows Feature -Name Web-Server
	```

7. Creamos un sitio nuevo llamado asir2, :

	```
New-WebSite -Name "asir2" -Port 80 -HostHeader "www.asir.com" -PhysicalPath "c:\inetpub\wwwroot"

	```



# Información adicional

- [How to manage IIS websites with Powershell.](https://www.business.com/articles/powershell-manage-iis-websites/)
- [PowerShell and IIS: 20 Practical examples](https://octopus.com/blog/iis-powershell)

