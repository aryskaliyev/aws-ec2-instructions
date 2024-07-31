### AWS EC2 Instructions

#### Update the package list
- `sudo apt update`
- `sudo apt upgrade -y`

#### Install NodeJS and npm
- `sudo apt install nodejs npm -y`

#### To deploy NextJS application
- git clone your repo
- `npm install`
- `npm run build`

#### Setup a reverse proxy with Nginx
- `sudo apt install nginx -y`

#### Configure Nginx
- `sudo vim /etc/nginx/sites-available/default`
```
server {
    listen 80;

    server_name <YOUR_DOMAIN> <YOUR_INSTANCE_PUBLIC_IP>;

    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

#### Restart Nginx
- `sudo systemctl restart nginx`

#### Secure application with HTTPS
- `sudo apt install certbot python3-certbot-nginx -y`
- `sudo certbot --nginx`

#### Installing and using PM2
- `sudo npm install -g pm2`
- `pm2 start npm --name "nextjs-app" -- start`
- `pm2 save`
- `pm2 startup`
	- View logs - `pm2 logs`
	- Check application status - `pm2 status`
	- Restart applciation - `pm2 restart nextjs-app`
	- Stop application - `pm2 stop nextjs-app`
	- Delete application - `pm2 delete nextjs-app`
