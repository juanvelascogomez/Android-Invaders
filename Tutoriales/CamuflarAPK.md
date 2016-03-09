#Como camuflar un apk maligno dentro de otro

Los pasos a seguir serían:

1. Creamos 3 carpetas para tenerlo todo organizado, estas serán: buena (aquí metemos el apk dentor de la cual queremos camuflar nuestra apk maliciosa), mala (aquí metemos el apk maliciosa que queremos camuflar) y combinada (aquí sera donde crearemos la nueva apk)

2. Descomprimir los APK, cada una en su carpeta:
	- Entramos en buena y ejecutamos:

			apktool d Good_app.apk  (siendo Good_app.apk nuestro apk buena)

	esto nos creará una carpeta al lado con el nombre de la app, en nuestro caso Good_app

	- Entramos en mala y ejecutamos:

			apktool d Bad_app.apk  (siendo Bad_app.apk nuestro apk buena)

	esto nos creará una carpeta al lado con el nombre de la app, en nuestro caso Bad_app

3. Copiar la carpeta Good_app (la de la aplicacion buena) en la carpeta de combinada

4. Meter la carpeta mala/Bad_app/smali/com/metasploit dentro de combinada/Good_app/smali/com

5. Accedemos a el archivo /com/metasploit/stage/MainActivity.smali y copiamos la línea en la que hay un "->start" que sería la que lanza nuestro proceso malicioso.

6. En nuestra Good_app buscamos el archivo que se lanza al inicar la app y dentro de él, el metodo OnCreate y dentro de el pegamos la linea que hemos copiado en 5. Esto hará que nuestra app maliciosa se lance al lanzarse la aplicación buena.

7. Ahora es el momento de añadir los permisos a nuestra app combinada para poder acceder a lo que queramos, como esto es un ejemplo, pondremos todos los que trae meterpreter por defecto, pero en la practica se puede poner solo la camara, o solo el microfono, etc.

	Abrimos el archivo de AndroidManifest.xml que hay dentro de la carpeta Bad_app y copiamos los permisos (lineas que empiezan por <uses-permission android...) en el AndroidManifest.xml que hay dentro de combinada/Good_app.

8. Recompilamos la app usando, dentro de combinada la orden:

		apktool b Good_app/

	Esto nos crea un apk en combinada/Good_app/dist/ que cogeremos y sacaremos a el directorio combinada para trabajar con él.

9. Vamos a firmar la app, para ello creamos una carpeta keys en combinada y nos situamos en combinada para trabajar.

10. Generamos la firma para nuestra app con:

  		keytool -genkey -v -keystore keys/Good_app.keystore -alias Good_app -keyalg RSA -keysize 2048 -validity 10000

	Rellenamos los parametros como queramos, incluso podemos copiar los de la app original.

11. Firmamos la app con:

  		jarsigner -verbose -keystore keys/Good_app.keystore Good_app.apk Good_app
