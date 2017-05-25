# Apache

Instalamos:
  apt-get install apache2
  
Creamos los directorios para las paginas web y aplicamos los permisos:

  sudo mkdir -p /var/www/escherichiacoli.es/html  
  sudo mkdir -p /var/www/chip555.org/html
  sudo mkdir -p /var/www/gato.com/html  
  sudo mkdir -p /var/www/mosquito.com/html 
  
  sudo chmod -R 777 /var/www
  
Creamos los sitios web y los configuramos por defecto:
  
  echo "Escherichiacoli" > /var/www/escherichiacoli.es/html/index.html
  
  echo "Chip 555" > /var/www/chip555.org/html/index.html
  
  echo "Gato" > /var/www/gato.com/html/index.html
  
  echo "Mosquito" > /var/www/mosquito.com/html/index.html
  

              
  sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/escherichiacoli.es.conf
  sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/chip555.org.conf
  sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/gato.com.conf
  sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/mosquito.com.conf
 
 Ficheros:
     
   ESCHERICHIACOLI:
    
    www.escherichiacoli.es
    <VirtualHost *:80>
        ServerAdmin admin@escherichiacoli.es
        ServerName escherichiacoli.es
        ServerAlias www.escherichiacoli.es
        DocumentRoot /var/www/escherichiacoli.es/html
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>
  
  CHIP555:
  
    www.chip555.org
    <VirtualHost *:80>
        ServerAdmin admin@chip555.org
        ServerName chip555.org
        ServerAlias www.chip555.org
        DocumentRoot /var/www/chip555.org/html
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>
    
  GATO:
  
    www.gato.es
    <VirtualHost *:80>
        ServerAdmin admin@gato.com
        ServerName gato.com
        ServerAlias www.gato.com
        DocumentRoot /var/www/gato.com/html
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>
    
   MOSQUITO:
   
    www.mosquito.com
    <VirtualHost *:80>
        ServerAdmin admin@mosquito.com
        ServerName mosquito.com
        ServerAlias www.mosquito.com
        DocumentRoot /var/www/mosquito.com/html
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>
    
 Habilitamos los sitios web:
 
    sudo a2ensite escherichiacoli.es.conf
    sudo a2ensite chip555.org.conf
    sudo a2ensite gato.com.conf
    sudo a2ensite mosquito.com.conf
    
Deshabilitamos el sitio por defecto:  sudo a2dissite 000-default.conf

Hacemos restart al demonio:  sudo service apache2 restart

Creamos un archivo para guardar las contraseñas:

sudo htpasswd -c /var/www/escherichiacoli.com/passwords user1
sudo htpasswd  -c /var/www/escherichiacoli.com/passwords user2

Creamos la configuracion para las paginas:

    user1:
    <Directory /var/www/escherichiacoli.com/html>
      AuthType Basic
      AuthName "ACCESO RESTRINGIDO."
      AuthUserFile /var/www/escherichiacoli.com/passwords
      Require user user01
    </Directory>
    <Directory /var/www/escherichiacoli.com/html>        
      Options Indexes FollowSymLinks MultiViews
      AllowOverride  none
      Order Allow,deny
      allow from user1
    </Directory>

    user2:
    <Directory /var/www/chip555.org/html>
      AuthType Basic
      AuthName "ACCESO RESTRINGIDO."
      AuthUserFile /var/www/escherichiacoli.com/passwords
      Require valid-user
    </Directory>
    <Directory /var/www/chip555.org/html>        
      Options Indexes FollowSymLinks MultiViews
      AllowOverride  none
      Order Allow,deny
      allow from all
    </Directory>

