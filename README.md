# Qv2ray For linux

# Server:

https://privacymelon.com/how-to-setup-v2ray-ws-tls-cdn/

# Client:

qv2ray :

https://github.com/v2fly/v2ray-core/releases/tag/v4.31.0

https://github.com/Qv2ray/Qv2ray/releases/tag/v2.7.0

nekoray: 

https://github.com/MatsuriDayo/nekoray/releases

copy qv2ray.desktop to address /home/{your home folder}/.local/share/applications






از این دو روش استفاده کن 
برای  Bridge زدن هم ۲ تا روش وجود داره که میتونید ازش استفاده کنید : 


1. Screen 
به سرور داخلیتون وصل شید 

و بعد توی اسکرین یه پورتی که میخواید رو با پورتی که روی سرور خارجیتون لیسن میشه  به ssh بدید  :
 
sudo screen ssh -o GatewayPorts=true -N -L 80:0.0.0.0:80 USER@External-IP
 
توی این قسمت 80:0.0.0.0 پورتی و آیپی لوکال هاست که روی سیستم باز میشه برای فورواد و :80 پورتی که روی سرویس وی پی ان اتون ران هست که دیفالت  80 هستش

و بعد پنجره ببنید که روی سرور ران باشه

2. Nginx

install : 
sudo apt install nginx

config : 
sudo nano /etc/nginx/nginx.conf

 این رو به ته خط اضافه کنید: 

stream {
    upstream external {
        server IP:PORT;  }
    server {
        listen     8080;
        proxy_pass external ; }  }
 
آی پی و پورت سرور خارجی مثلا v2ray یا شدوساکس رو تو این میزارید بعد میرید توی کلاینتتون ip و port شو ادیت میزنید تبدیل میکنید به این سرور ایرانی که اینجا تو مثال پورت 8080 گذاشتم . هرچی خواسید میتونید بزارید

reload service :

sudo systemctl reload nginx

در این روش اگر سرورتون هم ریست بخوره نیازی نیست که دوباره کامند screen رو بزنید :)


برای تونل زدن بین دو سرور
