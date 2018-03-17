# stock_pick
这是一个通过设定选股条件来帮我们筛选股票的python程序

	最近炒股是买什么就跌，一直是亏损，作为学过python的人来讲怎么能容忍，之前也炒过股票觉得用阳包阴这样的
k线来选出来的股票还不错。于是说做就做，我可以用python来写一个选股的程序。

	好！有了idea是第一步，要怎么实现呢，网上找了资料，大部分都是用tushare库来获取股票数据的。于是动起来
写了一个直接通过接口获取数据的程序，从3504只股票里面选取出来我需要的股票，执行时间居然需要二十多分钟，
太慢！差评！同样不能容忍。
	因此，我想到了数据库。我就想能不能将所有的A股数据添加进数据库里面，我每次执行的时候直接从数据库里面去取数据，
这样会大大加快了我的执行速度
	于是说干就干，先理清楚思路。
	
	1.需要获取到所有股票的代码跟名称等。于是有了write_allstock这个文件
	
	2.需要从所有的股票里面找出阳包阴的股票，以及计算出它们的收益率的话，我需要所有股票的一段时间的行情
	于是有了creat_everydatebase
	
	3.有了这一段时间的数据，但是这些数据时死了，不会每天给我自动更新，因此我需要每天定时的将当天的数据加
	进去。所以写了write_everyday
	
	4.好了，所有的股票数据一段时间的行情而且会每天定时更新都存在我的数据库里面了，就需要去统计今天有哪些股票满足
	阳包阴的情况于是产生了find_stock
	
	5.虽然找到了当天满足阳包阴的股票了，但是我心里还是没有谱，我想对比一下这个股票之前出现这种情况的时候如果
	第二天买入的话到底有多少收益，所以有了win_rates
	
	6.好了整体框架和思路都出来了，那么有两个文件需要每个交易日都执行的，所以将它们绑在一起，而且每天的报告出来
	之后也不一定都有时间打开电脑去看，所以加入了通过邮件自动发送当天报告到邮箱的功能。就有了run_all
	至于其它的几个文件，打开看看下面都有解释和注释
	

目前我的选股条件是阳包阴，而且当天要涨停。
