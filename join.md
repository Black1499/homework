##查询所有的广东省的省市以及省市县
####实现代码
	select c.id as id,p.cityName as province,c.cityName as city,null from s_provinces p
	inner join s_provinces c on p.id=c.parentid 
	where c.depth=2 and p.cityName='广东省'
	union
	select d.id as id,p.cityName as province,c.cityName as city,d.cityName as district from s_provinces d 
	inner join s_provinces c on c.id=d.parentid 
	inner join s_provinces p on p.id=c.parentid
	where c.depth=2 and p.cityName='广东省'; 
	
	
##具体思路以及遇到的困难
&emsp;&emsp;我最开始的思路是三个表一一关联进行查询，但是发现查到的都是省市县的数据，并没有老师要求的省市的数据，我想到了内连接是返回所有匹配的数据，所以不会出现省市的数据。于是我便采用了外连接的方式，无论是左外连接还是右外连接都没有拿到我想要的数据，思维便陷入了僵局。在老师的提醒下才想到了使用‘**union**’联合查询，先查到省市县的数据，再查到省市的数据。由于‘**union**’查询的前提是两个表的列的数量要一致，我便在查到的省市后面加了一个空列，为了便于区分，把省市县的id设为县的id,省市的id设为市的id,这样便不会产生id的冲突，保证了数据的唯一性。	