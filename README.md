Faça o clone do projeto:

Npm update;

Depois : 

sudo nano /etc/nginx/sites-available/api-zap
ou
cat > /etc/nginx/sites-available/api-zap

cole o conteudo abaixo:
server {

  server_name api-zap.fitlikeaglove.com.br;

  location / {

    proxy_pass http://127.0.0.1:3333;

    proxy_http_version 1.1;

    proxy_set_header Upgrade $http_upgrade;

    proxy_set_header Connection 'upgrade';

    proxy_set_header Host $host;

    proxy_set_header X-Real-IP $remote_addr;

    proxy_set_header X-Forwarded-Proto $scheme;

    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    
    proxy_cache_bypass $http_upgrade;

  }

 }
 
sudo ln -s /etc/nginx/sites-available/api-zap /etc/nginx/sites-enabled
sudo certbot --nginx
sudo service nginx restart
