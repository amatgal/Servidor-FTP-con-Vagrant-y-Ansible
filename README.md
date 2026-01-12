# 📦 Práctica: Vagrant + Ansible + FTP (anónimo y seguro)

Esta práctica consiste en desplegar un entorno automatizado usando **Vagrant y Ansible**  
y configurar en él dos servicios FTP:

- ✔️ FTP **anónimo**
- 🔐 FTP **seguro (FTPS)**

---

## 🧰 Tecnologías utilizadas
- Vagrant
- VirtualBox
- Ansible
- vsftpd
- OpenSSL (para FTPS)

## ⚙️ Aprovisionamiento con Ansible

El playbook principal ejecuta dos roles:

- ftp-anonimo

- ftp-seguro

Para reprovisionar manualmente:

    vagrant provision

## 🌐 3. FTP anónimo

El rol ftp-anonimo realiza:

- Instalación y activación del servicio vsftpd

- Habilita acceso anónimo

- Crea directorio público /srv/ftp

- Permite solo descarga

Acceso:

    ftp <IP_MAQUINA>
    usuario: anonymous
    contraseña: (vacío)

## 🔐 4. FTP seguro (FTPS)

El rol ftp-seguro:

- Activa usuarios reales del sistema

- Genera y utiliza certificado SSL

- Obliga conexión cifrada (TLS/SSL)

- Permite subida y descarga

Acceso recomendado con FileZilla:

- Protocolo: FTP sobre TLS

- Puerto: 21

- Usuario: usuario definido en VM

## 🧪 5. Pruebas
FTP anónimo en consola
    ftp <IP>

FTP seguro con lftp
    lftp -u usuario,pass -e "set ftp:ssl-force true" <IP>