# gulan.eu

# How to migrate form old hosting/vps to new one

1. Import old mysql db to new db
```
docker-compose exec db sh -c 'mysql -uroot -p${MYSQL_ROOT_PASSWORD} wordpress < /var/lib/mysql/gulan.sql'
```
2. Set wp_options 
```
docker-compose exec db sh -c 'mysql -uroot -p${MYSQL_ROOT_PASSWORD}'
update wp_options set option_value = 'http://193.46.198.195' where option_name = 'home';
update wp_options set option_value = 'http://193.46.198.195' where option_name = 'siteurl';
```
4. Comment condition in wp-config.php
```
//if (isset($_SERVER['HTTP_X_FORWARDED_PROTO']) && strpos($_SERVER['HTTP_X_FORWARDED_PROTO'], 'https') !== false) {
	$_SERVER['HTTPS'] = 'on';
//}
```
5. Upload old wordpress file and setup rights and replace old wp-config.php with new wp-config.php from this repo
```
docker exec -it vps-wordpress-1 /bin/bash
chown -R www-data:www-data /var/www/html/wp-content/
```
