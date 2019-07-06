# UT2: Instalación y configuración de uns servidor DNS en Windows mediante comandos Powershell. 

Continuamos en esta unidad utilizando Powershell para automatizar la instalación y configuración de servicios en Windows. Esta vez vamos a trabajar con DNS. 
Como en el caso anterior, necesitaremos un servidor que disponga de un dirección IP estática antes de proceder a la instalación de ningún servicio. También debemos comprobar si el servicio está o no instalado. En caso de que lo esté, lo vamos a desinstalar, reiniciaremos el servidor e instalaremos el servidor para comprobar el funcionamiento de todos los cmdlets. 

1. Comprobamos la **configuración de red**. La obtenemos en formato tabla para facilatar la lectura. Si el -PrefixOrigin es manual significa que la IP es estática.
 
	```
	Get-NetIPAddress -AddressFamily IPv4 |ft
	```

2. Configuramos la dirección **IP manual** en caso de que no lo sea. 

	```
	New-NetIPAddress -IPAddress 10.0.0.1 -InterfaceAlias "Ethernet" -DefaultGateway 10.0.0.254 -AddressFamily IPv4 -PrefixLength 24
	```
	Y añadimos el servidor DNS:
	
	```
	Set-DnsClientServerAddress -InterfaceAleas "Ethernet" -ServerAddresses 10.0.1.48
	```

3. **Comprobar** si el rol DNS está instalado. 

	```
	Get-WindowsFeature -name dns
	```

4. Si está instalado (quizás lo has instalado gráficamente), vamos a **desinstalar el rol**. 

	```
	Uninstall-WindowsFeature -Name dns
	```

5. **Reiniciamos** el servidor:
	
	```
	Restart-Computer
	```

6. **Instalamos el rol** DNS. Para ello debes comprobar previamente el nombre del rol. Lo puedes obtener a partir del comando observando la segunda columna:
	
	```
	Get-WindowsFeature 
	```
	Y ya puedes instalarlo: 
	
	```
	Install-WindowsFeature -Name dns
	```
	Y compruebas que está instalado:

	```
	Get-Windows Feature -Name dns
	```

7. Creamos una nueva **zona directa**. En nuestro caso se llamará asir.com. 

	```
	Add-DnsServerPrimaryZone -Name "asir.com" -ZoneFile "asir.com.dns"
	```

8. Creamos la **zona inversa** correspondiente. 

	```
	Add-DnsServerPrimaryZone -NetworkId "10.0.0.0/24" -ZoneFile "0.0.10.in-addr.dns"
	```

9. Comprobamos que las zonas han sido creadas: 
	
	```
	Get-DnsServerZone
	```
10. Ahora añadiremos **registros tipo A**. El nombre del equipo es pc1 y su dirección IP es 10.0.0.10:
	
	```
	Add-DnsServerResourceRecord -ZoneName "asir.com" -A -Name "pc1" -IPAddress "10.0.0.10"
	```
	También se podría haber utilizado el siguiente cmdlet:
	
	```
	Add-DnsServerResourceRecorda -Name "pc1" -ZoneName "asir.com" -IPv4Address "10.0.0.10"
	```
	
11. Añadimos **registros tipo CNAME** para pc1. El nombre del alias será pepe:
	
	```
	Add-DnsServerResourceRecordCname -Name "pepe" -HostNameAlias "pc1" -ZoneName "asir.com"
	```
12. Añadimos **registros tipo CNAME**:
	
	```
	```
13. Añadimos **registros tipo NS**:

	```
	```
14. Añadimos **registros tipo PTR**:
	
	```
	```

15. Comprobamos los registros que hemos añadido:
	
	```
	```
16. Configuramos un **reenviador**:

	``` html
<font color="red"> command </font>
```
	```
	```
17. wasdf


