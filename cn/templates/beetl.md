# 集成beetl

## 基本信息

* 官网 http://ibeetl.com/
* 下载 http://ibeetl.com/download/file.html

## 方案1, beetl官方方案

在MainModule声明:

```
@Views({BeetlViewMaker.class})
```

然后就可以在入口方法用了

```
@Ok("beetl:/templates/hello.html")
```

## 方案2, nutzbook改造版

在编写本小节的时候,我发现beetl一些问题(或许是我还没搞明白的地方):

* 内置的ResourceLoader均以File作为查找单位,这导致一些问题, 例如依赖绝对路径,部署时war不解压会读取不到
* 无日志机制
* getOutputStream或getWriter总会被调用,导致其他代码无法sendError或调用这两个方法
* BeetlViewMaker 不能配置自定义的ResourceLoader

所以我弄了3个类(当前均在net.wendal.nutzbook.beetl下), 事实上是重写了一次beetl插件

* BeetlViewMaker2 使其能自定义ResourceLoader
* ServletContextResourceLoader 通过ServletContext.getResourceAsStream 加载模板,解决war不解压时出现的问题,同时不需要依赖绝对路径
* LogErrorHandler 把日志通过nutz的Log类输出去

## 在MainModule声明:

```
@Views({BeetlViewMaker2.class})
```

## 在conf目录beetl.properties下添加配置文件

```
ERROR_HANDLER=net.wendal.nutzbook.beetl.LogErrorHandler
RESOURCE_LOADER=net.wendal.nutzbook.beetl.ServletContextResourceLoader
RESOURCE.root=/WEB-INF/templates/beetl
```

## 在目录 /WebContent/WEB-INF/templates/beetl 下添加一个模板, hello.html

```
总共 ${obj.list.~size}
<%
for(user in obj.list){
%>
hello,${user.nickname};


<%}%>

当前页${obj.pager.pageNumber},总共${obj.pager.pageCount}页
```

## 新建个BeetlTemplateModule类,加入下述方法

```
	@At
	@Ok("beetl:hello.html") // 可以简写为 @Ok("beetl:hello")
	@Fail("void") // beelt的机制导致只能使用void,详细原因看nutzbook中的代码吧
	public Object hello() {
		QueryResult qr = new QueryResult();
		Pager pager = dao.createPager(1, 20);
		pager.setRecordCount(dao.count(UserProfile.class));
		qr.setPager(pager);
		qr.setList(dao.query(UserProfile.class, null, pager));
		return qr;
	}
```

访问该入口方法即可看到效果

### 注意, 我并不确定方案1好还是方案2好,静待社区的反馈

## 可能出现的问题

* 找不到模板, 如果是方案一, 需要在beetl.properties中把RESOURCE.root设置为绝对路径
* 如果是方案二, 只能是写错路径或遇到bug了,欢迎报issue