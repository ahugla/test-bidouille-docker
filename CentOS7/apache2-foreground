#!/bin/bash




#get Tito code
if [ -z "$(ls -A /var/www/html)" ]; then
  git clone https://github.com/vmeoc/Tito /var/www/html/
  rm -Rf /var/www/html/asset/Deployment /var/www/html/.gitignore
fi

#if the env variable TITO_VERSION is available, then checkout the needed version.
if [ -n "$TITO_VERSION" ]; then
  cd /var/www/html/
  git pull
  git checkout $TITO_VERSION
fi


# Rendre executable le script Python de Tracing
chmod 777 /var/www/html/sendTraces.py


# WAVEFRONT CONFIG - set variable for apache in "/etc/sysconfig/httpd"
echo "PROXY_NAME=$PROXY_NAME" >> /etc/sysconfig/httpd
echo "PROXY_PORT=$PROXY_PORT" >> /etc/sysconfig/httpd


systemctl start httpd


# pour que le process ne s'arrete pas et que le container ne termine pas
tail -f /dev/null