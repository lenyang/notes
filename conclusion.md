<!-- MarkdownTOC -->

- 2018.9月
- 知识点一、生成按时间增长的全局唯一主键
- 知识点二、数组 array\(\) ,与 \[\] 的区别
- 知识点三、表单提交接收可变的参数
- 知识点四、php显示日期汇总
- 知识点五、Trait的应用
- 知识点六、 getallheaders\(\)函数
- 知识点七、解析 将导出的sql文件中的数据解析成数据数组
- 知识点八、Sphinx 全文搜索引擎（另一个可了解solr）

<!-- /MarkdownTOC -->

##2018.9月
#知识点一、生成按时间增长的全局唯一主键
用来生成按时间增长的全局唯一主键。这类主键的作用主要是在分布式环境中保证每条数据能够有一个唯一标识，同时又有一定的自增长性以提高索引效率。当然也可以用来掩人耳目，毕竟一个简单的int类型的自增ID的话，很容易让人猜到你的数据量有多少了。
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

#知识点二、数组 array() ,与 [] 的区别
```php
 $list = array(); #推荐
 $list=[];
```
以上两种表达方式的区别

#知识点三、表单提交接收可变的参数
下述方法可以用于接收可变的参数，有则写入数组，没有就跳过，最适用就是在修改数据表的数据时只更新修改的字段
```php
$updateArr = array();
foreach (array($val1,$val2,$val3,$val4) as $value) {
    $temp = $request->input($value,'');
    if(!empty($temp)){
        $updataArr[$value] = intval($temp);
    }
}
```

#知识点四、php显示日期汇总
```php
//今天
$today = date("Y-m-d");
//昨天
$yesterday = date("Y-m-d", strtotime(date("Y-m-d"))-86400);
//上周
$lastweek_start = date("Y-m-d H:i:s",mktime(0, 0 , 0,date("m"),date("d")-date("w")+1-7,date("Y")));
$lastweek_end = date("Y-m-d H:i:s",mktime(23,59,59,date("m"),date("d")-date("w")+7-7,date("Y")));
//本周
$thisweek_start = date("Y-m-d H:i:s",mktime(0, 0 , 0,date("m"),date("d")-date("w")+1,date("Y"))); 
$thisweek_end = date("Y-m-d H:i:s",mktime(23,59,59,date("m"),date("d")-date("w")+7,date("Y"))); 
//上月
$lastmonth_start = date("Y-m-d H:i:s",mktime(0, 0 , 0,date("m")-1,1,date("Y"))); 
$lastmonth_end = date("Y-m-d H:i:s",mktime(23,59,59,date("m") ,0,date("Y"))); 
//本月
$thismonth_start = date("Y-m-d H:i:s",mktime(0, 0 , 0,date("m"),1,date("Y"))); 
$thismonth_end = date("Y-m-d H:i:s",mktime(23,59,59,date("m"),date("t"),date("Y"))); 
//本季度未最后一月天数 
$getMonthDays = date("t",mktime(0, 0 , 0,date('n')+(date('n')-1)%3,1,date("Y")));
//本季度/
$thisquarter_start = date('Y-m-d H:i:s', mktime(0, 0, 0,date('n')-(date('n')-1)%3,1,date('Y'))); 
$thisquarter_end = date('Y-m-d H:i:s', mktime(23,59,59,date('n')+(date('n')-1)%3,$getMonthDays,date('Y')));
 
 
//2016-08-10这天 2个月后的日期
echo date("Y-m-d",strtotime("+2 month",strtotime("2018-09-19")));
     
//当前 3个月后的日期
echo date("Y-m-d",strtotime("+3 month",time()));

/**
     *  方法名 ：time_slot
     *  作  用 ：时间段（本日，昨日，本周，上周，本月，上月）
     *  @param ：
     *  @return： 返回时间段
     *  @author：
     *  @date  ：2016/7/14
     */
function time_slot(){
    $time['today']['begin'] = mktime(0,0,0,date('m'),date('d'),date('Y'));
    $time['today']['end'] = mktime(0,0,0,date('m'),date('d')+1,date('Y'))-1;
    $time['tomorrow']['begin'] =  mktime(0,0,0,date('m'),date('d')-1,date('Y'));
    $time['tomorrow']['end'] =  mktime(0,0,0,date('m'),date('d'),date('Y'))-1;
    $time['week']['begin'] = mktime(0, 0 , 0,date("m"),date("d")-date("w")+1,date("Y"));
    $time['week']['end'] = mktime(23,59,59,date("m"),date("d")-date("w")+7,date("Y"));
    $time['lastweek']['begin'] = mktime(0,0,0,date('m'),date('d')-date('w')+1-7,date('Y'));
    $time['lastweek']['end'] = mktime(23,59,59,date('m'),date('d')-date('w')+7-7,date('Y'));
    $time['month']['begin'] = mktime(0,0,0,date('m'),1,date('Y'));
    $time['month']['end'] = mktime(23,59,59,date('m'),date('t'),date('Y'));
    $time['lastmonth']['begin'] = mktime(0, 0 , 0,date("m")-1,1,date("Y"));
    $time['lastmonth']['end'] = mktime(23,59,59,date("m") ,0,date("Y"));
    //返回时间段
    return $time;
}
```
#知识点五、Trait的应用
    --a、Traits 是一种为类似PHP的单继承语言而准备的代码复用机制，Trait为了减少单继承语言的限制，使开发人员能够自由地在不同层次结构内独立的类中复用方法集。

    --b、Traits 和类组合的语义是定义了一种方式来减少复杂性，避免传统多继承和混入类（Mixin）相关的典型问题

    --c、Traits 和一个类相似，但仅仅旨在用细粒度和一致IDE方式来组合功能，Traits 不能通过它自身来实例化，它为传统继承增加了水平特性的组合：也就是说，应用类的成员不需要继承

    --d、 Trait 是在PHP5.4中加入的，它既不是接口，也不是类。主要是为了解决单继承语言的限制。是PHP多重继承的一个解决方案。例如 需要同时继承两个Abstract Class ，这将是件很麻烦的事情，Trait 就是为了解决这个问题，它能被加入到一个或多个已经存在的类中，它声明了类能做什么(表明了其接口特性)，同时也包含了具体实现(表明了其类特性) 
    --f、扩展链接 https://baijiahao.baidu.com/s?id=1588680671477174571&wfr=spider&for=pc


#知识点六、 getallheaders()函数
    apache 服务器专用函数库
    getallheaders(void);
    返回值：数组
    函数种类：PHP系统函数
    内容说明：使用本项功能时不需要带入任何参数值，返回的是所有HTTP变量值，数组返回
    示例：
        ```php
            $headers = getallheaders();
            while(list($header,$value) = each($headers)){
                echo  "$header:$value <br>";
            }

            //补充 getallheaders 兼容Nginx服务器
            function getallheaders(){
                foreach($_SERVER as $name =>$value){
                    if(substr($name,0,5) == 'HTTP_'){
                        $headers[str_replace('.','-',ucwords(strtolower(str_replace('_','.',substr($name,5)))))] = $value;
                    }
                }
                return $headers;
            }
        ```
#知识点七、解析 将导出的sql文件中的数据解析成数据数组
```php
function parseSql($filename)
{
    $lines    = file($filename);
    $lines[0] = str_replace(chr(239) . chr(187) . chr(191), "", $lines[0]); //去除BOM头
    $flage    = true;
    $sqls     = array();
    $sql      = "";
    foreach ($lines as $line) {
        $line = trim($line);
        $char = substr($line, 0, 1);
        if ($char != '#' && strlen($line) > 0) {
            $prefix = substr($line, 0, 2);
            switch ($prefix) {
                case '/*':
                    {
                        $flage = (substr($line, -3) == '*/;' || substr($line, -2) == '*/') ? true : false;
                        break 1;
                    }
                case '--':break 1;
                default:
                    {
                        if ($flage) {
                            $sql .= $line;
                            if (substr($line, -1) == ";") {
                                $sqls[] = $sql;
                                $sql    = "";
                            }
                        }
                        if (!$flage) {
                            $flage = (substr($line, -3) == '*/;' || substr($line, -2) == '*/') ? true : false;
                        }

                    }
            }
        }
    }
    return $sqls;
}
```
#知识点八、Sphinx 全文搜索引擎（另一个可了解solr）
```php
/**
     * Sphinx全文搜索引擎
     * [getSearchWordWhere 搜索关键词]
     * @param  [type] $q [关键词]
     * @return [type]    [返回查询数组
     */
    function getSearchWordWhere($q){
        //引人
        $where =[];
        if(file_exists(PLUGIN_PATH.'coreseek/sphinxapi.php')){
            require_once(PLUGIN_PATH.'coreseek/sphinxapi.php');
            $c1 = new \SphinxClient();
            $c1->setServer(C('SPHINX_HOST').'',intval(C('SPHINX_HOST')));
            $c1->setConnectTimeout(10);
            $c1->SetArrayResult(true);
            $c1->SetMatchMode(SPH_MATCH_ANY);
            $res = $c1->Query($q,'mysql');
            if($res){
                $goods_id_array = array();
                if(array_key_exists('matches',$res)){
                    foreach ($res['matches'] as $key => $value) {
                        $goods_id_array[] = $value['id'];
                    }

                }
                if(!empty($goods_in_array)){
                    $where['goods_id'] = array('in',$goods_id_array);
                }else{
                    $where['goods_id'] = 0;
                }
            }else{
                $q_arr = explode('',$q);
                foreach ($q_arr as $key => $value) {
                    $q_arr[$key] = '%'.$value.'%';
                }
                $where['goods_name'] = array('like','%'.$q.'%');
            }
            return $where;
        }
    }

```
# 知识点九 redis 的持续化pconnection 时，选择db ，出现读写不再同一个db
>redis 中 pconnection  与 connection 的区别，如果处于pconnect 的情况下，持续链接的时候，选择db 的时候会默认选择0 db ，如果存在redis共用的情况下，不止链接默认db 的时候 ，那么，下次默认写入的时候，会随机从db 0 和db 1中选一个出来，
>解决：直接在读写的时候都指定选择一个db
```sql
    redis::select(1);
```