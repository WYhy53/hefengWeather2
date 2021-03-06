# hefengWeather2
//已经有了新版本,加入了显示逐小时整点时刻天气状况的功能,详情请访问https://github.com/WYhy53/hefengWeather3

风和日丽天气是一款基于Android端开源的天气预报软件,具备查看全国的省市县、查询任意城市天气、自由切换城市、手动更新天气、后台自动更新天气和背景图片等功能.风和日丽中的天气数据由和风日丽天气提供,城市数据由郭霖老师《第一行代码》上面的API提供,背景图片由必应提供,代码遵循Apache v2 License开源协议.


使用步骤及功能介绍:

通过城市选择按钮从对应的省市县列表中选择的城市从而展示对应城市的天气数据.右上角表示对应展示的天气数据的更新的时间,往下依次是此时的实况天气,当天和未来两天天气预报和当日生活建议.


![image](https://github.com/WYhy53/UIPractice/blob/master/hefeng.gif)


使⽤到的⽐较重要的技术及知识点：

1.创建数据库和表，使用LitePal来管理数据库.

2.使用HTTP协议访问网络，使用okHttp，在子线程更新UI.

3.使用JSONObject和GSON来解析JSON格式数据.

4.使用SharedPreference存储数据.

5.下拉刷新.

6.后台服务自动更新.


⼼得体会：

本app大部分代码基于《第一行代码》上面的酷欧天气实战,(但绝对没有直接复制粘贴),所不同的是在获得天气数据、定义GSON实体类、展示天气界面和后台服务自动更新天气方法这一部分,作了较大改动.

虽然和风天气上提供了城市搜索功能,但鉴于需要对请求参数进行 url encode相比郭霖老师的方法较复杂一些且与我之前app的功能——展示城市列表而非搜索相冲突,所以还是决定采用郭霖老师在《第一行代码》上面遍历全国省市县数据的方法.由于和风天气是根据你请求的“weather-type”不同,将返回基本参数和不同的具体天气数据,而我所需要的的天气数据正是对应3个不同的“weather-type”,所以需要3个不同的API进行网络请求,网络请求部分由郭霖老师对应的WeatherID转化为WeatherName——对应点击城市的名字.依次将解析后的数据通过SharedPreference使用同一个key键值储存,对应的展示天气界面的方法也分为对应的3个不同的方法一一加载不同的天气布局.在有缓存直接解析天气数据时再通过相同的key键值取出全部的数据,再调用总的展示全部天气界面的方法将总的天气界面展示出来.
