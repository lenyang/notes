##2018.9月
#知识点一、
今天写了个简单的PHP函数，用来生成按时间增长的全局唯一主键。这类主键的作用主要是在分布式环境中保证每条数据能够有一个唯一标识，同时又有一定的自增长性以提高索引效率。当然也可以用来掩人耳目，毕竟一个简单的int类型的自增ID的话，很容易让人猜到你的数据量有多少了。
分布式环境下数据主键的生成方法其实是蛮多的，比如使用Mysql之类的自增ID，只需要设置好自增步长和起始值就可以满足基本要求了，还有像目前流行的文档型数据库MongoDB就提供了一个MongoId的实现，可以在客户端直接生成长度为24的自增长型全局字符串主键。今天写的这个PHP函数就是参考MongoId的算法实现的，不需要安装MongoDB扩展也可以使用。
MongoDB的PHP扩展中有一个C语言版本的 generate_id 函数的实现，可以参考 https://github.com/mongodb/mongo-php-driver/blob/master/types/id.c。基本上，每个 MongoId 具有 12 个字节（使它的字符串形式是 24 个十六进制字符），前四个字节是一个时间戳（timestamp int，单位为秒），后三个是客户端主机名的 hash 摘要，然后两个是运行脚本的进程 ID， 最后三位是一个以随机数作为起始值的自增值。从这个描述里我们也可以看出，MongoId的生成基本是向上增长的，也不太可能出现重复，是一个比较优质的主键生成实现。
eg：
```php
function generate_id_hex()
{
    static $i = 0;
    $i OR $i = mt_rand(1, 0x7FFFFF);
 
    return sprintf("%08x%06x%04x%06x",
        /* 4-byte value representing the seconds since the Unix epoch. */
        time() & 0xFFFFFFFF,
 
        /* 3-byte machine identifier.
         *
         * On windows, the max length is 256. Linux doesn't have a limit, but it
         * will fill in the first 256 chars of hostname even if the actual
         * hostname is longer. 
         *
         * From the GNU manual:
         * gethostname stores the beginning of the host name in name even if the
         * host name won't entirely fit. For some purposes, a truncated host name
         * is good enough. If it is, you can ignore the error code.
         *
         * crc32 will be better than Times33. */
        crc32(substr((string)gethostname(), 0, 256)) >> 8 & 0xFFFFFF,
 
        /* 2-byte process id. */
        getmypid() & 0xFFFF,
 
        /* 3-byte counter, starting with a random value. */
        $i = $i > 0xFFFFFE ? 1 : $i + 1
    );
}

for ($j=0; $j <100 ; $j++) { 
	echo generate_id_hex();
	echo "<br>";
	# code...
}
exit;
```