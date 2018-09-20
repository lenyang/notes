##PHP
# bug.1
问题：php7.2报错 the each() function is deprecated . this message will be suppreseed on furthe
原因：php7.2将each方法废除了 
解决: foreach() 方法去替换 each()

# bug.2
 问题：Laravel 出现 “RuntimeException inEncrypter.php line 43 : The only supported ciphers are AES-128-CBC and AES-256-CBC with the correct key lengths.”
 原因：Laravel 中的 APP_KEY
 解决：
 	在项目目录下执行 php -artisan key:generate 如果还是报错，那就要从别的项目里去复制一个key到.env中，然后再运行命令：composer update 和 php artisan key:generate 这样key就变掉了。