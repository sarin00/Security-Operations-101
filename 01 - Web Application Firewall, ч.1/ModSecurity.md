## 1. Що таке Web Application Firewall (WAF)?
WAF, або фаєрвол для феб-застосунків - це такий інструмент який потрібен для захисту ваших веб застосунків від деяких атак. WAF працює на Application рівні в TCP/IP та OSI моделях. Більшість WAF концентрується на HTTP/HTTPS трафіку, перевіряючи його та шукаючи збіги з правилами які ви налаштовуєте. 

Ваші програми дуже різні, і що нормально для однієї програми є аномалією для іншої. Загрози вашій програмі не тільки унікальні для вас, але й відрізняються між компонентами вашої ж системи (наприклад, що є прийнятним для одного API ендпоінта неприйнятно для іншого). Це означає, що немає універсальних налаштувань WAF, які б працювали для всіх і відбивали б усі атаки. Ми повинні також створювати власні правила виключно під наші програми та їх компоненти разом.

## 2. Хід роботи
1. Підняти віртуальну машину з Ubuntu  
2. [Встановити на Ubuntu OWASP Juice shop](https://pwning.owasp-juice.shop/companion-guide/latest/part1/running.html)  
```
# Встановити Docker Engine  
sudo apt install docker.io  

# Завантажити імедж контейнеру з juice-shop  
docker pull bkimminich/juice-shop

# Запустити контейнер  
docker run -d -p 127.0.0.1:3000:3000 bkimminich/juice-shop  
```
3. [Встановити веб сервер, що буде працювати як reverse proxy для вашого juiceshop аплікейшину (nginx або apache)](https://github.com/sarin00/Course1-Intro-to-Cybersecruity/blob/main/11%20%D0%9F%D0%97%20-%20%D0%92%D0%B5%D0%B1%20%D1%81%D0%B5%D1%80%D0%B2%D0%B5%D1%80%2C%20%D0%B2%D0%B5%D0%B1%20%D0%B7%D0%B0%D1%81%D1%82%D0%BE%D1%81%D1%83%D0%BD%D0%BE%D0%BA%2C%20%D1%97%D1%85%20%D0%B1%D0%B5%D0%B7%D0%BF%D0%B5%D0%BA%D0%B0/Web%20app%2C%20nginx%2C%20SSL%20certs.md#6-%D0%BF%D1%80%D0%B0%D0%BA%D1%82%D0%B8%D1%87%D0%BD%D0%B5-%D0%B7%D0%B0%D0%B2%D0%B4%D0%B0%D0%BD%D0%BD%D1%8F)  
```
# Встановити nginx
sudo apt install nginx

# Редагувати конфіг nginx
nano /etc/nginx/sites-available/default

# Додати в конфіг в секціїю location наступні дані:
server_name yourdomain.com www.yourdomain.com;

 location / {
        proxy_pass http://localhost:3000; #port for juice-shop
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
```
4. [Виконати кілька атак на веб застосунок щоб перевірити працездатність та вразливість застосунку](https://pwning.owasp-juice.shop/part1/running.html)  
5. [Встановити оупенсорсний WAF (web application firewall) ModSecurity під обраний вами веб сервер](https://github.com/owasp-modsecurity/ModSecurity-nginx)  
6. [Налаштувати ModSecurity правила для вловлення базових веб атак](https://owasp.org/www-project-modsecurity-core-rule-set/)  
7. Проаналізувати ефективність WAF

Основна задача цього заняття це зрозуміти, як само WAF інстурменти можуть допомагати нам захщати веб застосунки та навчитись налаштовувати безкоштовний WAF ModSecurity.
