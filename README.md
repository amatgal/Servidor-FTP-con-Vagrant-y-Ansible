📦 Práctica: Vagrant + Ansible + FTP (anónimo y seguro)

Este proyecto despliega un entorno automatizado con Vagrant y Ansible, configurando dos servicios FTP:

✔️ FTP anónimo (solo descarga)

🔐 FTP seguro (FTPS) con usuarios locales

🧰 Tecnologías

Vagrant + VirtualBox

Ansible

vsftpd

OpenSSL (certificado autofirmado para FTPS)

⚙️ Aprovisionamiento

Para crear y configurar todo:

vagrant up
vagrant provision


Esto instalará vsftpd, creará usuarios (luis, maria, miguel), configurará FTP anónimo y FTPS con certificado SSL.

🌐 FTP anónimo

Directorio público: /srv/ftp

Usuario: anonymous

Contraseña: (vacío)

Solo descarga de archivos

Ejemplo de prueba:

ftp <IP_VM>
ls
put prueba.txt   # ❌ Denegado

🔐 FTP seguro (FTPS)

Usuarios locales con contraseña:

luis:luis123 (enjaulado)

miguel:miguel123 (enjaulado)

maria:maria123 (no enjaulada)

Certificado autofirmado en /etc/ssl/certs/example.test.pem

Conexión obligatoria cifrada para usuarios locales

Ejemplo de prueba con lftp:

lftp -u luis,luis123 ftp://<IP_VM>
set ssl:verify-certificate no   # ignorar error de certificado autofirmado
ls
put prueba.txt   # ✅ funciona
get luis1.txt    # ✅ funciona


Usuarios anónimos siguen teniendo solo lectura.

🧪 Comportamiento esperado
Usuario	Permisos	Enjaulado
anonymous	descarga únicamente	n/a
luis	descarga y subida	sí
miguel	descarga y subida	sí
maria	descarga y subida	no

💡 Nota: El certificado es autofirmado; para conexiones seguras desde clientes como lftp es necesario desactivar temporalmente la verificación de certificado (set ssl:verify-certificate no).
