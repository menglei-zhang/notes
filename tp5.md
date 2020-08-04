#### 数据库
### 控制器
### 模型

### 查询数据 find select 
### 添加数据 insert insertAll
### 更新数据 update setField
    ## 自增或者自减 setInc setDes
    ## 延时更新 setInc('score',1,10)   10s后给score字段增加1
### 删除数据 delete
### 查询方法
    ## 条件查询  
        where 
            where('username','like','%zhang')->where('satus',1)
            where()

            where('username','like','zhang')->whereOr('title','like','zhang')
            <==>
            where('username|title','like','zhang')
        
        where 和 whereOr  混合查询
        $result = Db::table('think_user')->where(function ($query) {
            $query->where('id', 1)->whereor('id', 2);
        })->whereOr(function ($query) {
            $query->where('name', 'like', 'think')->whereOr('name', 'like', 'thinkphp');
        })->select();
        生成的sql语句类似于下面：
        SELECT * FROM `think_user` WHERE  (  `id` = 1 OR `id` = 2 ) OR (  `name` LIKE 'think' OR `name` LIKE 'thinkphp' )


数据库新增列  alter table TABLE_NAME add column NEW_COLUMN_NAME varchar(40) not null;


$data = json_decode(file_get_contents("php://input"), true);

$outcome = $data->allowField(true)->isUpdate(true)->save($list);

###  事务  
$users = new Users();
$users -> startTrans();
$users -> commit();
$users -> rollback();





一个软件产品从开发到用户使用都涉及哪些环境？	开发环境、测试环境、回归环境、预发布环境、生产环境。

PHP中预定义了几个超级全局变量（superglobals） ，这意味着它们在一个脚本的全部作用域中都可用。 你不需要特别说明，就可以在函数及类中使用。
PHP 超级全局变量有: $GLOBALS 、$_SERVER 、$_REQUEST 、$_POST、$_GET 、$_FILES、$_ENV、$_COOKIE、$_SESSION。
超级全局变量在PHP 4.1.0之后被启用, 是PHP系统中自带的变量，在一个脚本的全部作用域中都可用。

if($this->request->isPost()){
	$data = input('post.');
	$user = Db::name('users')->where('id',$data['user_id'])->find();
}


// 输出验证数据格式
public function echoArr($code,$msg,$data = []){
	return [
		'code' => $code,
		'msg' => $msg,
		'data' => $data
	];
}


### 入口文件
ThinkPHP采用 单一入口模式 进行项目部署和访问，无论完成什么功能，一个应用都有一个统一(但不是唯一)的入口。

### URL访问
ThinkPHP5.0在没有启用路由的情况下典型的URL访问规则是：
http://serverName/index.php（或者其它应用入口文件）/模块/控制器/操作/[参数名/参数值...]    pathinfo

## 隐藏入口文件
下面是Apache的配置过程，可以参考下：
1、httpd.conf配置文件中加载了mod_rewrite.so模块
2、AllowOverride None 将None改为 All
3、在应用入口文件同级目录添加.htaccess文件，内容如下：

遵循ThinkPHP5.0的命名规范，模块目录全部采用小写和下划线命名。
common模块是一个特殊的模块，默认是禁止直接访问的，一般用于放置一些公共的类库用于其他模块的继承。
ThinkPHP5采用命名空间方式定义和自动加载类库文件，有效的解决了多模块和Composer类库之间的命名空间冲突问题，并且实现了更加高效的类库自动加载机制。


### 路由
## 路由模式
	thinkphp 5.0 的路由比较灵活，并且不需要强制定义，可以总结归纳为如下三种方式
	1、普通模式
		关闭路由 使用默认的PATH_INFO方式URL：
		'url_route_on' => false,
		关闭路由后不会解析任何的路由规则，采用默认的PATH_INF模式访问URL
		http://serverName/入口文件/模块/控制器/方法/参数/值
		http://serverName/index.php/module/controller/action/param/value/...
		但是任然可以通过操作方法的参数绑定、空控制器、空方法 等特性实现URL地址的简化
		可以设置 url_param_type 配置参数来改变pathinfo 模式下面的参数获取方式，默认是按名称成对解析，支持按照顺序解析变量
		'url_param_type' => 1,    // 按照顺序解析变量
	2、混合模式
		开启路由，并使用理由定义+默认PATH_INFO 方式的混合
		'url_route_on' => true,
		'url_route_must' => false,
		该方式下面，只需要对需要定义路由规则的访问地址定义路由规则，其它的仍然按照第一种普通模式的PATH_INFO模式访问URL。
	3、强制模式
		开启路由，并设置必须定义才能访问
		'url_route_on' => true,
		'url_route_must' => true,
		这种方式下面必须严格给每一个访问地址定义路由规则（包括首页），否则将抛出异常。
		首页的路由规则采用/定义即可，例如下面把网站首页路由输出Hello,world!
		Route::get('/',function(){
			return 'Hello,world!';
		});
## 路由定义
	路由注册可以采用方法动态单个和批量注册，也可以直接定义路由定义文件的方式进行集中注册
	动态注册： 
	路由定义采用 \think\Route 类的 rule 方法注册，通常是在用用的路由配置文件application/toute.php 进行注册
	Route::rule('理由表达式','路由地址','请求类型','路由参数（数组）','变量规则（数组）');

	use think\Route;

	Route::rule('new/:id','index/News/read');
	// ThinkPHP5.0的路由规则定义是从根目录开始，而不是基于模块名的。

	访问：http://serverName/new/5
	==>>
	http://serverName/index/new/read/id/5

	原来的访问地址会失效


	可以在rule方法中指定请求类型，不指定的话默认为任何请求类型
	Route::rule('new/:id','News/update','POST');

	GET    POST    PUT    DELETE    *     // 请求类型参数必须大写

	统提供了为不同的请求类型定义路由规则的简化方法
	Route::get('new/:id','News/read'); // 定义GET请求路由规则
	Route::post('new/:id','News/update'); // 定义POST请求路由规则
	Route::put('new/:id','News/update'); // 定义PUT请求路由规则
	Route::delete('new/:id','News/delete'); // 定义DELETE请求路由规则
	Route::any('new/:id','News/read'); // 所有请求都支持的路由规则

	如果要定义get和post请求支持的路由规则
	Route::rule('new/:id','News/read','GET|POST');

	批量注册路由规则：
	Route::rule(['new/:id'=>'News/read','blog/:name'=>'Blog/detail']);
	Route::get(['new/:id'=>'News/read','blog/:name'=>'Blog/detail']);
	Route::post(['new/:id'=>'News/update','blog/:name'=>'Blog/detail']);

## 路由表达式
	规则表达式通常包含静态地址和动态地址，或者两种地址的结合

	'/' => 'index', // 首页访问路由
	'my'        =>  'Member/myinfo', // 静态地址路由
	'blog/:id'  =>  'Blog/read', // 静态地址和动态地址结合
	'new/:year/:month/:day'=>'News/read', // 静态地址和动态地址结合
	':user/:blog_id'=>'Blog/read',// 全动态地址

	可选定义
	'blog/:year/[:month]'=>'Blog/archive',
	[:month]变量用[ ]包含起来后就表示该变量是路由匹配的可选变量

	http://serverName/index.php/blog/2015
	http://serverName/index.php/blog/2015/12

	采用可选变量定义后，之前需要定义两个或者多个路由规则才能处理的情况可以合并为一个路由规则。

	可选参数只能放到路由规则的最后，如果在中间使用了可选参数的话，后面的变量都会变成可选参数

	完全匹配
	规则匹配检测的时候只是对URL从头开始匹配，只要URL地址包含了定义的路由规则就会匹配成功，如果希望完全匹配，可以在路由表达式最后使用$符号

	'new/:cate$'=> 'News/category',
	http://serverName/index.php/new/info	// 会匹配成功
	http://serverName/index.php/new/info/2  // 不会匹配成功
	如果是采用   'new/:cate'=> 'News/category',
	方式定义的话，则两种方式的URL访问都可以匹配成功。

	如果你希望所有的路由定义都是完全匹配的话，可以直接配置

	// 开启路由定义的全局完全匹配
	'route_complete_match'  =>  true,

	当开启全局完全匹配的时候，如果个别路由不需要使用完整匹配，可以添加路由参数覆盖定义：

	Route::rule('new/:id','News/read','GET|POST',['complete_match' => false]);


	额外参数
	在路由跳转的时候支持额外传入参数对（额外参数指的是不在URL里面的参数，隐式传入需要的操作中，有时候能够起到一定的安全防护作用，后面我们会提到）。例如：

	'blog/:id'=>'blog/read?status=1&app_id=5',
	上面的路由规则定义中额外参数的传值方式都是等效的。status和app_id参数都是URL里面不存在的，属于隐式传值，当然并不一定需要用到，只是在需要的时候可以使用。


## 批量注册
	如果不希望一个个注册，可以使用批量注册，规则如下：
	Route::rule([
	'路由规则1'=>'路由地址和参数',
	'路由规则2'=>['路由地址和参数','匹配参数（数组）','变量规则（数组）']
	...
	],'','请求类型','匹配参数（数组）','变量规则');


#### 控制器
	控制器类可以无需任何类，命名空间默认以 app 为根命名空间
	如果继承了 think\Controller 类的话，可以直接调用 think\View 及 think\Request 类的方法

	<?php
		namespace app\admin\controller;

		use think\Controller;

		public function index()
		{
			$this->assign('domain',$this->request->url(true));
			return $thin->fetch('index');
		}

	?>

	默认情况下，控制器的输出全部采用 return 的形式，无需进行任何的手动输出，系统会自动完成渲染内容的输出

	默认情况下，控制器的返回输出不会做任何的数据处理，但可以设置输出格式，并进行自动的数据转换处理，前提是控制器的输出数据必须采用return的方式返回

	控制器初始化

	如果控制器类继承了 \think\Controller 类的话，可以定义控制器初始化方法 _initialize , 在该控制器的方法调用之前首先执行

	public function _initialize()
	{
		echo "init";
	}

	前置操作

	可以为某个或者某些操作指定前置执行的操作方法，设置beforeActionList属性可以指定某个方法为其他方法的前置操作，数组键名为需要调用的前置方法名，无值的话为当前控制器下所有方法的前置方法。

	['except' => '方法名,方法名']   // 表示这些方法不使用前置方法，

	['only' => '方法名,方法名']    // 表示只有这些方法使用前置方法。

## 前置操作
可以为某个或者某些操作指定前置执行的操作方法，设置 beforeActionList属性可以指定某个方法为其他方法的前置操作，数组键名为需要调用的前置方法名，无值的话为当前控制器下所有方法的前置方法。

## 页面跳转
在应用开发中，经常会遇到一些带有提示信息的跳转页面，例如操作成功或者操作错误页面，并且自动跳转到另外一个目标页面。系统的\think\Controller类内置了两个跳转方法success和error，用于页面跳转提示。

## 重定向
\think\Controller类的redirect方法可以实现页面的重定向功能。
redirect方法的参数用法和Url::build方法的用法一致（参考URL生成部分）

## 空操作
空操作是指系统在找不到指定的操作方法的时候，会定位到空操作（_empty）方法来执行，利用这个机制，我们可以实现错误页面和一些URL的优化。

## 空控制器
空控制器的概念是指当系统找不到指定的控制器名称的时候，系统会尝试定位空控制器(Error)，利用这个机制我们可以用来定制错误页面和进行URL的优化。





## 请求
如果要获取当前的请求信息，可以使用\think\Request类，
$request = Request::instance();

## 输入变量
可以通过Request对象完成全局输入变量的检测、获取和安全过滤，支持包括$_GET、$_POST、$_REQUEST、$_SERVER、$_SESSION、$_COOKIE、$_ENV等系统变量，以及文件上传信息。


## 系统变量输出
普通的模板变量需要首先赋值后才能在模板中输出，但是系统变量则不需要，可以直接在模板中输出，系统变量的输出通常以 "{$Think"  打头，例如：
{$Think.server.script_name} // 输出$_SERVER['SCRIPT_NAME']变量
{$Think.session.user_id} 	// 输出$_SESSION['user_id']变量
{$Think.get.pageNumber} 	// 输出$_GET['pageNumber']变量
{$Think.cookie.name}  		// 输出$_COOKIE['name']变量
支持输出 $_SERVER、$_ENV、 $_POST、 $_GET、 $_REQUEST、$_SESSION和 $_COOKIE变量。

## 请求参数
模板支持直接输出Request请求对象的方法参数，用法如下：$Request.方法名.参数
{$Request.get.id}
{$Request.param.name}
以$Request.开头的变量输出会认为是系统Request请求对象的参数输出。

支持Request类的大部分方法，但只支持方法的第一个参数。

{$create_time|date="y-m-d",###}

{$status? '正常' : '错误'}
{$info['status']? $info['msg'] : $info['error']}
{$info.status? $info.msg : $info.error }

## 模板继承
一个模板中可以定义任意多个名称标识不重复的区块，例如下面定义了一个base.html基础模板：

<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>{block name="title"}标题{/block}</title>
</head>
<body>
{block name="menu"}菜单{/block}
{block name="left"}左边分栏{/block}
{block name="main"}主内容{/block}
{block name="right"}右边分栏{/block}
{block name="footer"}底部{/block}
</body>
</html>

然后我们在子模板（其实是当前操作的入口模板）中使用继承：

{extend name="base" /}
{block name="title"}{$title}{/block}
{block name="menu"}
<a href="/" >首页</a>
<a href="/info/" >资讯</a>
<a href="/bbs/" >论坛</a>
{/block}
{block name="left"}{/block}
{block name="main"}
{volist name="list" id="vo"}
<a href="/new/{$vo.id}">{$vo.title}</a><br/>
 {$vo.content}
{/volist}
{/block}
{block name="right"}
 最新资讯：
{volist name="news" id="new"}
<a href="/new/{$new.id}">{$new.title}</a><br/>
{/volist}
{/block}
{block name="footer"}
{__block__}
 @ThinkPHP 版权所有
{/block}

### 内置标签
## VOLIST标签
	{volist name = 'list' id = 'vo'}
		{$vo.name}
	{/volist}

	支持输出查询结果中的部分数据，例如输出其中的第5～15条记录
	{volist name="list" id="vo" offset="5" length='10'}
		{$vo.name}
	{/volist}

## FOREACH标签   foreach标签类似与volist标签，只是更加简单，没有太多额外的属性，最简单的用法是：
	{foreach $list as $vo} 
		{$vo.id}:{$vo.name}
	{/foreach}
	该用法解析后是最简洁的。

	也可以使用下面的用法：

	{foreach name="list" item="vo"}
		{$vo.id}:{$vo.name}
	{/foreach}
	name表示数据源 item表示循环变量。

	可以输出索引，如下：

	{foreach name="list" item="vo" }
		{$key}|{$vo}
	{/foreach}
	也可以定义索引的变量名

	{foreach name="list" item="vo" key="k" }
	{$k}|{$vo}
	{/foreach}

## FOR标签
	{for start="开始值" end="结束值" comparison="" step="步进值" name="循环变量名" }
	{/for}
	开始值、结束值、步进值和循环变量都可以支持变量，开始值和结束值是必须，其他是可选。comparison 的默认值是lt，name的默认值是i，步进值的默认值是1，举例如下：

	{for start="1" end="100"}
	{$i}
	{/for}
	解析后的代码是

	for ($i=1;$i<100;$i+=1){
		echo $i;
	} 

## 比较标签
	{eq name="name" value="value"}value{/eq}
	





	$data = input('input.');   // 一次传过来好多input表单值

	tp5的Request::instance()获取post、get、参数、表单上传的文件
	$request = Request::instance();
    $method = $request->method();//获取上传方式
    $request->param();//获取所有参数，最全
    $get = $request->get();获取get上传的内容
    $post = $request->post();获取post上传的内容
    $request->file('file')获取文件

	<?php 
		namespace app\index\controller; 
		use think\Request; 
		class Index 
		{ 
		public function index(Request $request) 
		{ 
			# 获取浏览器输入框的值 
			dump($request->domain()); 
			dump($request->pathinfo()); 
			dump($request->path()); 
			
			# 请求类型 
			dump($request->method()); 
			dump($request->isGet()); 
			dump($request->isPost()); 
			dump($request->isAjax()); 
			
			# 请求的参数 
			dump($request->get()); 
			dump($request->param()); 
			dump($request->post()); 
			//session('name', 'onestopweb'); 
			//cookie('email', 'onestopweb@163.com'); 
			//session(null); 
			//cookie('email',null); 
			dump($request->session()); 
			dump($request->cookie()); 
			
			dump($request->param('type')); 
			dump($request->cookie('email')); 
			
			# 获取模块 控制器 操作 
			dump($request->module()); 
			dump($request->controller()); 
			dump($request->action()); 
			
			# 获取URL 
			dump($request->url()); 
			dump($request->baseUrl()); 
		} 
	}
	
	
	
    file:model/Users.php
    <?php
        namespace app\admin\model;
        use think\Model;
        use app\admin\validate\Users as Vali;
        class Users extends Model
        {
            public fucntion operation($data){
                $validate = new Vali();
                if(!$validate -> check($data)){
                    return echoArr(0,$validate->getError());
                }
                // allowField : 过滤非数据表字段  ;   
                $res = $this -> allowField(true) -> isUpdate(true) -> save($data);
                if($res === false){
                    return echoArr(0,$this->getError());
                }else{
                    return echoArr(1,'操作成功');
                }
            }
        }
        
        $this->request->isAjax()
        $data = input();
        $data = input('post.');
        $data = $this->request->post();
        
        数据验证
        
        controller
        // 验证数据格式
        $result = $this->validate($data, 'AdminUser.login');
        if(true !== $result){
            // 验证失败 输出错误信息
            return $this->error($result, '', ['token' => $this->request->token()]);
        }
        
        model
        $validate = new Vali();
        if(!$validate -> check($data)){
            return echoArr(0,$validate->getError());
        }
        
        $this->success('退出成功','index/index');
        
        
        
        
    


