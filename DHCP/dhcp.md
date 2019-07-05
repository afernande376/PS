# UT1: Instalción y configuración de un servidor DHCP en Windows

Vamos a aprender a realizar la configuración de un servidor DHCP en Windows, pero en vez de utilizar el entorno gráfico lo realizaremos mediante comandos de Powershell. 
La instalación  configuración del rol DHCP medianet comandos Powershell se puede realizar de dos maneras:
** Localmente
** Remotamente

En esta ocuasión veremos cómo realizaralo localmente. Recuerda que antes de comenzar a trabajar, debes disponer de la misma informacion previa que necesitarías en caso de realizar la configuración de manualmente, es decir, necesitas:

* Servidor configurado con una dirección IP estática. 
* Nombre del ámbito o ámbitos. 
* Rango de IPs de cada ámbito. 
* Puerta de enlace de cada ámbito. 
* Dirección IP del Servidor DNS.
* Máscara de red. 
* Otras opciones que se requiera como podría ser el nombre de dominio. 

Una vez que dispongas de toda la información ya puedes proceder a seguir los pasos para instalar un servidor DHCP utilizando comandos Powershell:

1. Abre un terminal de PowerShell con permisos de administrador. 

2. Configura una dirección IP estática para el servidor:

```
New-NetIPAddress -IPAddress 10.0.0.1 -InterfaceAlias "Ethernet" -DefaultGateway 10.0.0.254 -AddressFamily IPv4 -PrefixLength 24
```
Y añadimos el servidor DNS:

```
Set-DnsClientServerAddress -InterfaceAleas "Ethernet" -ServerAddresses 10.0.1.48
```


3. Comprobar si el rol DHCP está instalado. 

```
Get-WindowsFeature -name dhcp

```

2. Si está instalado (quizás lo has instalado gráficamente), lo vamos a desinstalar. 

```
Uninstall-WindowsFeature -Name dhcp

```

3. Reiniciamos el servidor:

```
Restart-Computer
```

4. Instalamos el rol DHCP. Para ello debes comprobar previamente el nombre del rol. Lo puedes obtener a partir del comando observando la segunda columna:

```
Get-WindowsFeature 
```
Y ya puedes instalarlo:

```
Install-WindowsFeature 

```
Y compruebas que está instalado:

```
Get-Windows Feature -Name dhcp
```

5. Añadimos un nuevo ámbito que se llamará asir2, que entregará direcciones en el rango 10.0.0.100 a 10.0.0.200 de la subred /24 y finalmente lo activamos:

```
Add-DhcpServerv4Scope -Name "asir2" -StartRage 10.0.0.100 -EndRange 10.0.0.200 -SubnetMask 255.255.255.0 -State Active
```
6. Ahora vamos a excluir por ejemplo la dirección 10.0.0.150:
```
Add-DhcpServerv4ExclusionRange -ScopeId 10.0.0.0 -StartRange 10.0.0.150 -EndRange 10.0.0.150
```

7. Añadimos un servidor DNS para el ámbito:

```
Add-DhcpServerv4ExclusionRange -ScopeId 10.0.0.0 -StartRange 10.0.0.150 -EndRange 10.0.0.150

```

8. Y añadimos una opción para el ámbito, por ejemplo, el sufijo DNS "asir.com":

```
Set-DhcpServerv4OptionValue -DnsServer 10.0.1.48 -DnsDomain asir.com
```

