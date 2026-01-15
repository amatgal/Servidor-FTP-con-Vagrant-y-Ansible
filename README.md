📦 Práctica: Vagrant + Ansible + FTP (anónimo y seguro)

Esta práctica despliega un entorno automatizado con Vagrant y Ansible, configurando dos servicios FTP:

✔️ FTP anónimo (solo lectura)

🔐 FTP seguro (FTPS) con usuarios locales y certificado SSL/TLS

🧰 Tecnologías utilizadas

Vagrant + VirtualBox

Ansible

vsftpd

OpenSSL (para FTPS)

⚙️ Aprovisionamiento

Ejecuta desde el directorio del proyecto:

vagrant up
vagrant provision


Esto hará:

Instalación de vsftpd

Creación de usuarios locales (luis, maria, miguel)

Configuración de directorios y archivos de prueba

Generación de certificado SSL autofirmado

Configuración de FTP anónimo y FTPS

Reinicio del servicio

🌐 FTP anónimo

Directorio público: /srv/ftp

Usuario: anonymous

Contraseña: (vacío)

Solo permite descarga de archivos, subida denegada

Prueba rápida:
ftp <IP_VM>
ls
put prueba.txt   # ❌ Denegado

🔐 FTP seguro (FTPS)

Usuarios locales:

luis:luis123 (enjaulado en su home)

miguel:miguel123 (enjaulado en su home)

maria:maria123 (no enjaulada)

Certificado SSL: /etc/ssl/certs/example.test.pem

Requisito: Conexión cifrada TLS/SSL para usuarios locales

Prueba con lftp:
lftp -u luis,luis123 ftp://<IP_VM>
set ssl:verify-certificate no   # Ignorar error de certificado autofirmado
ls
put prueba.txt   # ✅ Permite subir
get luis1.txt    # ✅ Permite descargar


Usuarios anónimos siguen teniendo solo lectura.

🧪 Comportamiento esperado
Usuario	Permisos	Enjaulado
anonymous	descarga únicamente	n/a
luis	descarga y subida	sí
miguel	descarga y subida	sí
maria	descarga y subida	no
💡 Notas importantes

El certificado es autofirmado; por eso los clientes como lftp pueden dar error de verificación.

Para probar FTPS desde la consola, usar:

set ssl:verify-certificate no


En entornos reales se debería usar un certificado emitido por una autoridad de confianza (CA).
