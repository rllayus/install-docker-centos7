# install-docker-centos7
Instalación de docker en centos 7


https://www.hostinger.es/tutoriales/instalar-docker-centos7


https://www.osradar.com/install-docker-and-manage-it-with-portainer-on-centos-8-rhel-8/


#Verificar con que usuario se ejecuta jboss en el contenedor con el siguiente comando y acuerdo al usuario ejecutar el comando para verificar el gid
id -g jboss y id -u jboss

#Crear un usuario con el mismo uid/gid en el host con los siguientes comando

groupadd -r jboss -g 1000
useradd -u 1000 -r -g jboss -s /sbin/nologin -c "Registros de contenedores de WildFly" wildfly-logs

chown administrador /var/log/clic
chcon -t svirt_sandbox_file_t /var/log/clic

#Comando para iniciar el contenedor con el volumen
docker run -p 8080:8080 -p 9990:9990 -p 8443:8443 -d -v /var/log/clic:/opt/jboss/wildfly/standalone/log/  --name clic wildfly /opt/jboss/wildfly/bin/standalone.sh -b 0.0.0.0 -bmanagement 0.0.0.0


https://goldmann.pl/blog/2014/07/18/logging-with-the-wildfly-docker-image/
