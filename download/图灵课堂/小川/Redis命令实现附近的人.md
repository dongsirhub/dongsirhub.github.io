# Redis命令实现附近的人

获取经纬度：[http://api.map.baidu.com/lbsapi/getpoint/index.html](http://api.map.baidu.com/lbsapi/getpoint/index.html)

经纬度验证：[https://tool.lu/coordinate/](https://tool.lu/coordinate/)

+ <font style="color:rgb(0, 0, 0);">GEOADD: 将给定的位置对象（纬度、经度、名字）添加到指定的key;</font>
+ <font style="color:rgb(0, 0, 0);">GEOPOS: 从key里面返回所有给定位置对象的位置（经度和纬度）;</font>
+ <font style="color:rgb(0, 0, 0);">GEODIST: 返回两个给定位置之间的距离;</font>
+ <font style="color:rgb(0, 0, 0);">GEORADIUS: 以给定的经纬度为中心，返回目标集合中与中心的距离不超过给定最大距离的所有位置对象;</font>

## 使用前必读
1. **运行代码前，需要获取百度地图的ak；**
2. **获取ak步骤，访问：**[**https://lbsyun.baidu.com/index.php?title=jspopularGL/guide/getkey#service-page-anchor2**](https://lbsyun.baidu.com/index.php?title=jspopularGL/guide/getkey#service-page-anchor2)

**(白名单可以直接填*)**

3. **获取到ak之后，在项目中的location.html找到"百度地图ak"字样，然后将他替换成自己的百度地图ak即可**

## <font style="color:rgb(36, 41, 47);background-color:rgb(244, 246, 248);">1.添加用户的位置信息</font>
<font style="color:rgb(36, 41, 47);background-color:rgb(244, 246, 248);">使用GEOADD命令向地理信息中添加用户的位置信息。</font>

```plain
GEOADD user_location <经度> <纬度> <用户ID>
```

<font style="color:rgb(36, 41, 47);background-color:rgb(244, 246, 248);">例如，添加用户“user1”的位置信息：</font>

```plain
GEOADD city 113.871021 22.581088 userId1 #广东:深圳:宝安:天虹商场
GEOADD city 113.869692 22.582556 userId2#广东:深圳:宝安:脱单公社
GEOADD city 114.123319 22.538368 userId3 #广东:深圳:罗湖区:火车站
GEOADD city 113.869669 22.582769 userIdr4 #广东:深圳:宝安:西乡公交站
GEOADD city 121.503541 31.246287 userId5 #上海:浦东新区:东方明珠游船码头
GEOADD city 121.542101 31.2419 uuserId6 #上海:浦东新区:陆家嘴国际华城
GEOADD city 116.302269 39.99242 userId7 #北京:海淀区:海淀公园
GEOADD city 112.985314 28.198102 userId8 #湖南:长沙:芙蓉区:长沙IFS国金中心
GEOADD city 112.888347 28.213122 userId9 #湖南:长沙:岳麓区:麓谷企业广场
GEOADD city 112.909133 28.19954 userId10  #湖南:长沙:岳麓区:梅溪湖公园

#整合成一条命令
GEOADD city 113.871021 22.581088 userId1 113.869692 22.582556 userId2 
114.123319 22.538368 userId3 113.869669 22.582769 userId4 121.503541 31.246287 userId5 121.542101 31.2419 uuserId6 
116.302269 39.99242 userId7 112.985314 28.198102 userId8 112.888347 28.213122 userId9 
112.909133 28.19954 userId10
```

<font style="color:rgb(36, 41, 47);background-color:rgb(244, 246, 248);">Java代码</font>

```java
Point point = new Point(longitude, latitude);
RedisGeoCommands.GeoLocation<Object> location = new RedisGeoCommands.GeoLocation<>(userId, point);
//GEOADD user_location <经度> <纬度> <用户ID>
redisTemplate.opsForGeo().add(KEY, location);
```

## <font style="color:rgb(36, 41, 47);background-color:rgb(244, 246, 248);">2.查询用户位置信息</font>
<font style="color:rgb(36, 41, 47);background-color:rgb(244, 246, 248);">使用GEOPOS命令查询指定用户的位置信息。</font>

```plain
GEOPOS user_location <用户ID>
```

<font style="color:rgb(36, 41, 47);background-color:rgb(244, 246, 248);">例如，查询用户“</font>userId1<font style="color:rgb(36, 41, 47);background-color:rgb(244, 246, 248);">”的位置信息：</font>

```plain
GEOPOS city userId3
```

<font style="color:rgb(36, 41, 47);background-color:rgb(244, 246, 248);">此命令会返回用户“user1”的经度和纬度坐标。</font>

<font style="color:rgb(36, 41, 47);background-color:rgb(244, 246, 248);">Java代码</font>

```java
List<Point> positionList = redisTemplate.opsForGeo().position(KEY, userId);
```

## <font style="color:rgb(0, 0, 0);">3.查询两个给定位置之间的距离</font>
<font style="color:rgb(36, 41, 47);background-color:rgb(244, 246, 248);">使用</font>GEODIST<font style="color:rgb(36, 41, 47);background-color:rgb(244, 246, 248);">命令查询两个给定位置直接的距离</font>

```plain
GEODIST user_location <用户ID> <用户ID> m 
```

其中，<font style="color:rgb(36, 41, 47);background-color:rgb(244, 246, 248);">m表示单位为米，也可以用km、ft、mi等表示</font>

<font style="color:rgb(36, 41, 47);background-color:rgb(244, 246, 248);">例如，查询距离（userId1 userId2）的距离：</font>

```plain
GEODIST city userId1 userId2 m
```

Java代码

```java
Distance distance = redisTemplate.execute(
    connection -> connection.geoDist(KEY.getBytes(), userId1.getBytes(), userId2.getBytes(), RedisGeoCommands.DistanceUnit.KILOMETERS), true);
```



## <font style="color:rgb(36, 41, 47);background-color:rgb(244, 246, 248);">4.查询附近的人</font>
<font style="color:rgb(36, 41, 47);background-color:rgb(244, 246, 248);">使用GEORADIUS命令查询附近指定经纬度坐标的人。</font>

```plain
GEORADIUS user_location l<经度> <纬度> <半径> m|km|ft|mi [WITHCOORD] [WITHDIST] [WITHHASH] [COUNT count] [ASC|DESC]
```

<font style="color:rgb(36, 41, 47);background-color:rgb(244, 246, 248);">其中，<经度>和<纬度>为指定的中心点坐标，<半径>为搜索半径（单位：米），m表示单位为米，也可以用km、ft、mi等表示；WITHDIST表示同时返回距离信息，WITHCOORD表示同时返回坐标信息。</font>WITHHASH表示<font style="color:rgb(36, 41, 47);background-color:rgb(244, 246, 248);">返回zset中的</font>score <font style="color:rgb(36, 41, 47);background-color:rgb(244, 246, 248);">。</font><font style="color:rgb(36, 41, 47);">COUNT</font><font style="color:rgb(36, 41, 47);background-color:rgb(244, 246, 248);"> 表示返回结果的数量限制。</font><font style="color:rgb(36, 41, 47);">ASC</font><font style="color:rgb(36, 41, 47);background-color:rgb(244, 246, 248);"> 和 </font><font style="color:rgb(36, 41, 47);">DESC</font><font style="color:rgb(36, 41, 47);background-color:rgb(244, 246, 248);"> 表示返回结果按距离从近到远或从远到近排序</font>

<font style="color:rgb(36, 41, 47);background-color:rgb(244, 246, 248);">例如，查询距离 </font>userId10<font style="color:rgb(36, 41, 47);background-color:rgb(244, 246, 248);">（</font>112.909133 28.19954<font style="color:rgb(36, 41, 47);background-color:rgb(244, 246, 248);">）坐标1000米以内的人：</font>

```plain
 GEORADIUS city 112.909133 28.19954 1 km WITHDIST WITHCOORD ASC COUNT 100 WITHHASH
```

Java代码

```java
  //表示圆形的查询条件,point坐标，distance:半径为 radius 单位(m,km...)的圆形
  Circle circle = new Circle(new Point(longitude, latitude), new Distance(radius, Metrics.KILOMETERS));
  //其他参数
   GeoRadiusCommandArgs args = GeoRadiusCommandArgs.newGeoRadiusArgs()
          //排序字段
          .sortDescending()
           //WITHDIST表示同时返回距离信息
          .includeDistance()
          //WITHCOORD表示同时返回坐标信息
          .includeCoordinates();
  GeoResults<RedisGeoCommands.GeoLocation<Object>> results = redisTemplate.opsForGeo().radius(KEY, circle, args);
        
```

<font style="color:rgb(36, 41, 47);background-color:rgb(244, 246, 248);">  
</font>



> 更新: 2023-04-28 17:10:25  
> 原文: <https://www.yuque.com/tulingzhouyu/sfx8p0/feqt5gguxpviar1l>