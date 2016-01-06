#ApacheBench测试

ab的全称是ApacheBench，是 Apache 附带的一个小工具，专门用于 HTTP Server 的benchmark testing，可以同时模拟多个并发请求。前段时间看到公司的开发人员也在用它作一些测试，看起来也不错，很简单，也很容易使用，所以今天花一点时间看了一下。ab 不像 LR 那么强大，但是它足够轻便，如果只是在开发过程中想检查一下某个模块的响应情况，或者做一些场景比较简单的测试，ab 还是一个不错的选择——至少不用花费很多时间去学习 LR 那些复杂的功能，就更别说那 License 的价格了 通过下面的一个简单的例子和注释，相信大家可以更容易理解这个工具的使用。


###例子

```
/*在这个例子的一开始，我执行了这样一个命令 ab -n 10 -c 10 http://www.google.com/。
这个命令的意思是启动 ab ，向 www.google.com 代表总共发出10个请求(-n 10) ，
并采用10个并发（-c 10模拟10个人同时访问)——也就是说一次都发过去了。*/
 
ab -n 10 -c 10 http://www.google.com/
 
This is ApacheBench, Version 2.0.40-dev <$Revision: 1.146 $> apache-2.0
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Copyright 1997-2005 The Apache Software Foundation, http://www.apache.org/
 
Benchmarking www.google.com (be patient).....done
 
 
Server Software:        GWS/2.1
Server Hostname:        www.google.com
Server Port:            80
 
Document Path:          /
Document Length:        230 bytes
 
Concurrency Level:      10
/*整个测试持续的时间*/
Time taken for tests:   3.234651 seconds
/*完成的请求数量*/
Complete requests:      10
/*失败的请求数量*/
Failed requests:        0
Write errors:           0
Non-2xx responses:      10
Keep-Alive requests:    10
/*整个场景中的网络传输量*/
Total transferred:      6020 bytes
/*整个场景中的HTML内容传输量*/
HTML transferred:       2300 bytes
/*大家最关心的指标之一，相当于 LR 中的 每秒事务数 ，后面括号中的 mean 表示这是一个平均值*/
Requests per second:    3.09 [#/sec] (mean)
/*大家最关心的指标之二，相当于 LR 中的 平均事务响应时间 ，后面括号中的 mean 表示这是一个平均值*/
Time per request:       3234.651 [ms] (mean)
/*这个还不知道是什么意思，有知道的朋友请留言，谢谢 ^_^ */
Time per request:       323.465 [ms] (mean, across all concurrent requests)
/*平均每秒网络上的流量，可以帮助排除是否存在网络流量过大导致响应时间延长的问题*/
Transfer rate:          1.55 [Kbytes/sec] received
/*网络上消耗的时间的分解，各项数据的具体算法还不是很清楚*/
Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:       20  318 926.1     30    2954
Processing:    40 2160 1462.0   3034    3154
Waiting:       40 2160 1462.0   3034    3154
Total:         60 2479 1276.4   3064    3184
 
/*下面的内容为整个场景中所有请求的响应情况。在场景中每个请求都有一个响应时间，
其中 50％ 的用户响应时间小于 3064 毫秒，60 ％ 的用户响应时间小于 3094 毫秒，
最大的响应时间小于 3184 毫秒。cpu实际上并不是同时处理的，
而是按照每个请求获得的时间片逐个轮转处理的，
所以基本上第一个Time per request时间约等于第二个Time per request时间乘以并发请求数。*/
Percentage of the requests served within a certain time (ms)
  50%   3064
  66%   3094
  75%   3124
  80%   3154
  90%   3184
  95%   3184
  98%   3184
  99%   3184
 100%   3184 (longest request)

```

###参数说明

```
产生的请求个数（并发数）。默认是一次一个。
-t timelimit Seconds to max. wait for responses
//测试所进行的最大秒数。其内部隐含值是-n 50000。
//它可以使对服务器的测试限制在一个固定的总时间以内。默认时，没有时间限制。
-p postfile File containing data to POST
//包含了需要POST的数据的文件，文件格式如“p1=1&p2=2”.使用方法是 -p 111.txt 。 （配合-T）
-T content-type Content-type header for POSTing
//POST数据所使用的Content-type头信息，如 -T “application/x-www-form-urlencoded” 。 （配合-p）
-v verbosity How much troubleshooting info to print
/*设置显示信息的详细程度 – 4或更大值会显示头信息， 3或更大值可以显示响应代码(404, 200等), 
2或更大值可以显示警告和其他信息。 -V 显示版本号并退出。*/
-w Print out results in HTML tables
//以HTML表的格式输出结果。默认时，它是白色背景的两列宽度的一张表。
-i Use HEAD instead of GET
// 执行HEAD请求，而不是GET。
-x attributes String to insert as table attributes
-y attributes String to insert as tr attributes
-z attributes String to insert as td or th attributes
-C attribute Add cookie, eg. -C “c1=1234,c2=2,c3=3″ (repeatable)
/*-C cookie-name=value 对请求附加一个Cookie:行。 
其典型形式是name=value的一个参数对。此参数可以重复，用逗号分割。*/
提示：可以借助session实现原理传递 JSESSIONID参数， 实现保持会话的功能，如
-C ” c1=1234,c2=2,c3=3, JSESSIONID=FF056CD16DA9D71CB131C1D56F0319F8″ 。
-H attribute Add Arbitrary header line, eg. ‘Accept-Encoding: gzip’ Inserted after all normal header lines. (repeatable)
-A attribute Add Basic WWW Authentication, the attributes
are a colon separated username and password.
-P attribute Add Basic Proxy Authentication, the attributes
are a colon separated username and password.
/*-P proxy-auth-username:password 对一个中转代理提供BASIC认证信任。
用户名和密码由一个:隔开，并以base64编码形式发送。
无论服务器是否需要(即, 是否发送了401认证需求代码)，此字符串都会被发送。*/
-X proxy:port Proxyserver and port number to use
-V Print version number and exit
-k Use HTTP KeepAlive feature
-d Do not show percentiles served table.
-S Do not show confidence estimators and warnings.
-g filename Output collected data to gnuplot format file.
-e filename Output CSV file with percentages served
-h Display usage information (this message)
/*-attributes 设置属性的字符串. 缺陷程序中有各种静态声明的固定长度的缓冲区。
另外，对命令行参数、服务器的响应头和其他外部输入的解析也很简单，这可能会有不良后果。
它没有完整地实现 HTTP/1.x; 仅接受某些’预想’的响应格式。
 strstr(3)的频繁使用可能会带来性能问题，即你可能是在测试ab而不是服务器的性能。 */
```
 
###进行post压力测试

apache的ab进行post压力测试

建创post文件
```
{"ID":"fiXwy47fbw,460013002605748,832980265625894,vpKAPfQJOC,1,MT801","GPS":"092000,11418.19593E,3036.26708N,0.00,0.557,450;092002,11418.19607E,3036.26706N,0.00,0.125,451;092004,11418.19645E,3036.26722N,0.00,0.120,451;092006,11418.19604E,3036.26762N,0.00,0.296,452;092008,11418.19572E,3036.26787N,0.00,0.231,452;092010,11418.19935E,3036.26764N,0.00,0.787,451;092012,11418.20002E,3036.26832N,60.60,1.200,452;092014,11418.20133E,3036.26789N,0.00,0.761,452;092016,11418.20191E,3036.26773N,0.00,1.205,452;092018,11418.20131E,3036.26760N,0.00,0.374,452;092020,11418.19527E,3036.26724N,0.00,0.146,453;092022,11418.19511E,3036.26711N,0.00,0.255,453;092024,11418.19593E,3036.26720N,0.00,0.700,453;092026,11418.19723E,3036.26751N,0.00,0.120,453;092028,11418.19857E,3036.26749N,0.00,0.138,453;092030,11418.19705E,3036.26501N,0.00,0.177,454;092032,11418.19677E,3036.26499N,0.00,0.262,454;092034,11418.19609E,3036.26553N,0.00,0.083,454;092036,11418.19575E,3036.26596N,0.00,0.340,454;092038,11418.19532E,3036.26650N,0.00,0.200,455;092040,11418.20859E,3036.26362N,0.00,0.340,456;092042,11418.20696E,3036.26335N,0.00,0.218,456;092044,11418.20453E,3036.26378N,0.00,0.088,456;092046,11418.20144E,3036.26546N,0.00,0.109,456;092048,11418.19872E,3036.26625N,0.00,1.114,457;092050,12122.11282E,3113.17707N,0.00,0.733,458;092052,12122.11355E,3113.17794N,0.00,0.268,458;092054,12122.11388E,3113.17876N,0.00,0.381,458;092056,12122.11396E,3113.17830N,0.00,0.290,458","GSENSOR":"092000000,9.5129,0.1340,-0.8135;9.5512,0.1148,-0.9283;9.5607,0.1148,-0.8422;9.6086,0.1436,-0.7848;9.6469,0.1340,-0.8709;9.6086,0.0957,-0.8613;9.5607,0.1053,-0.8709;9.6086,0.1340,-0.8518;9.5990,0.1340,-0.8230;9.6373,0.1340,-0.8613;9.5799,0.1148,-0.8805;9.6277,0.1053,-0.7943;9.5799,0.0957,-0.7848;9.6086,0.1053,-0.8326;9.5799,0.0957,-0.8039;9.6947,0.0670,-1.0240;9.6086,0.1244,-0.7656;9.5895,0.0766,-0.8613;9.6086,0.1148,-0.9666;9.5799,0.1148,-0.8422;9.6373,0.1436,-0.8518;9.5320,0.1053,-0.8613;9.5512,0.1148,-0.8709;9.6086,0.1148,-0.8422;8.9770,-0.0957,3.5602;8.9674,-0.0957,3.5697;8.9482,-0.0957,3.5793;8.9578,-0.1053,3.5506;8.9482,-0.1148,3.5793;092056000,9.1492,0.2584,2.8807"}
```
或
```
param1=a&param2=b&param3=c
```
注意：把post文件按照默认的ANSI编码形式进行保存，内容为`param1=a&param2=b&param3=c`。

性能测试
```
ab -c 10 -n 100 -p /home/post -T 'application/x-www-form-urlencoded' http://192.168.1.11:80/collectdata
```

####参数说明：

-c后面跟的是一次产生的请求个数

-n后面跟的是发送多少个请求（实际上就是把-n分批发送）

-p后面跟的是内容的目录

-T后面这个是明码的意思，可以不用管


###总结

总结：在远程对web服务器进行压力测试，往往效果不理想（因为网络延时过大），建议使用内网的另一台或者多台服务器通过内网进行测试，这样得出的数据，准确度会高很多。如果只有单独的一台服务器，可以直接本地测试，比远程测试效果要准确。


###来源

http://www.cnblogs.com/jackei/archive/2006/07/18/454144.html

http://www.ha97.com/4617.html

http://www.mirrtalk.net/?p=807
