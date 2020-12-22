sudo apachectl -k start
sudo apachectl -k restart
sudo apachectl -k stop

find storage -type d -exec chmod 777 {} \;
find storage -type f -exec chmod 777 {} \;

sudo /usr/local/mysql/support-files/mysql.server start;
sudo /usr/local/mysql/support-files/mysql.server stop;
sudo /usr/local/mysql/support-files/mysql.server restart;


创建项目： composer create-project --prefer-dist laravel/laravel blog

#### laravel 是一个 强规范约束 的框架，强制使用大量 预定义结构 来确保应用结构

### 目录结构
    app:
        bootstrap:包含框架启动、自动载入等基本逻辑
        config: 国有的配置项设置 
        database: 必要的 数据库模式迁移 以及 数据迁移逻辑
        public: Web目录的document根目录，包含 应用入口文件(index.php) 以及多有服务器assets，例如样式表和图像等
        resources: 视图(view) 国际化文件 以及 其他应用资源
        storage: 框架非应用的临时储存项 例如编译后的视图 会话数据 缓存数据 日志
        tests: 创建的所有自动化测试
        vendor: 多有通过Composer载入的应用依赖
        app: 应用的逻辑代码

### 应用Kernel类


### composer PHP的类库管理

#### 核心架构

### 生命周期

    Laravel 应用的所有请求入口都是 public/index.php 文件。
    这里是加载框架其它部分的起点。

    HTTP / Console  内核   作为所有请求都要通过的位置；



### 服务容器

laravel的服务容器是一个用于管理类依赖以及注入依赖的强有力工具
注入依赖：实质上是指 通过构造函数 或者 某些情况下 通过setter方法将类依赖注入到类中；







### 路由器 将用户的请求转发给相应的程序去处理  请求类型get,put,post,patch,delete等

tp: shop.com/index.php/模块/控制器/方法

laravel: shop.com/user/show

Route::get("user/show","UserController@show");

Route::get("/",function(){
    return view("welcome");
})


## 基础路由  laravel框架将请求传递给laravel路由器，该路由器将请求内容映射给应用中适当的控制器；
# Route::get()
# Route::post()
# Route::put()
# Route::delete()
# Route::any()
# Route::match()
# 正则限制  Route::get()->where(['id'=>'\d+','name'=>"[a-zA-Z]+"]);   ->where('id','[0-9]+')  ->where('name'=>"[a-zA-Z]+")
## 多请求路由
Route::match(["get","post"],"user/register",function(){
    return "register";
})
## Route::match();
    Route::match(['get','post'],'user/register',function(){
        return "register";
    });
## Route::any();
    Route::any("user/list",function (){
        return "user/list";
    });
## 路由传参(参数可选)
    Route::get("user/{id?}/{name}",function ($id = 1,$name){
        return "user_show_".$id."_".$name;
    });
## 正则限制
Route::get("user/{id}/{name}",function ($id,$name){
    return "user_".$id."_".$name;
})->where(['id'=>'\d+','name'=>"[a-zA-Z]+"]);

### 控制器 namespace App\Http\Controllers;
驼峰：首字母大写

php artisan make:controller UserController
php artisan make:controller Home/IndexController


Route::get("user/show","UserController@show");
Route::get("user/show","Admin\UserController@show");



$cname = $request -> input('data.cname');
$cname = $request -> input('cname');
$data1=$request->all();
$data2 = $request -> only('cname','parent_id','isrec');
$data3 = $request -> except('_token');
$file = $request -> file("photo");

### 中间件

中间件提供了一种方便的机制过滤进入应用程序的 HTTP 请求。
例如，Laravel 包含一个验证用户身份的中间件。 
如果用户未能通过认证，中间件会把用户重定向到登录页面。 反之，用户如果通过验证， 中间件将把请求进一步转发到应用程序中。

## 使用 make:middleware 命令来创建新的中间件:
php artisan make:middleware CheckAgeMiddleware
要让请求继续传递到应用层中（即允许「通过」中间件验证），只需要将 $request 作为参数来调用函数 $next 即可 。return $next($request);

public function handle($request, Closure $next)
{
    return $next($request);
}

## 前置 & 后置中间件
中间件是在请求之前或之后执行，取决于中间件本身。

public function handle($request, Closure $next)
{
    dump("hello");
    $res = $next($request);
    dump("hello");
    return $res;
}

## 注册中间件

# 如果没有在 App/Http/Kernel.php 文件内为该中间件分配一个键
Route::get('/midlle',['middleware'=>'App\Http\Middleware\EmailMiddleware',function(){ 
    echo 'luyou'; 
}]);

Route::get('/mi',['middleware'=>'App\Http\Middleware\EmailMiddleware','uses'=>'IndexController@mi']);   // 'uses'=>'控制器@方法名'

Route::get('/','IndexController@mi') -> middleware('App\Http\Middleware\EmailMiddleware');

# 全局中间件
如果你希望中间件在应用处理每个 HTTP 请求期间运行， 只需要在 app/Http/Kernel.php 中的 $middleware 属性中列出这个中间件。

protected $middleware = [
    \App\Http\Middleware\TrustProxies::class,
    \Fruitcake\Cors\HandleCors::class,
    \App\Http\Middleware\CheckForMaintenanceMode::class,
    \Illuminate\Foundation\Http\Middleware\ValidatePostSize::class,
    \App\Http\Middleware\TrimStrings::class,
    \Illuminate\Foundation\Http\Middleware\ConvertEmptyStringsToNull::class,
];

# 为路由分配中间件
假设你想为指定的路由分配中间件 ， 首先应该在 App/Http/Kernel.php 文件内为该中间件分配一个键。
默认情况下，该类中的 $routeMiddleware 属性下包含了 Laravel 内置的中间件。
若要加入自定义的中间件，只需把它附加到列表后并为其分配一个自定义键

# 一旦在 HTTP 内中定义好了中间件，就可以通过 middleware 方法为路由分配中间件：
Route::get('admin/profile', function () {
    //
})->middleware('auth');

# 也可以为路由分配多个中间件：
Route::get('/', function () {
    //
})->middleware('first', 'second');

# 分配中间件时，还可以传递完整的类名：
use App\Http\Middleware\CheckAge;
Route::get('admin/profile', function () {
    //
})->middleware(CheckAge::class);

# 中间件参数
中间件还可以接收额外的参数。
如果你的应用程序需要在执行给定操作之前验证用户是否为给定的(角色),可以创建一个 CheckRole 中间件，由它来接收(角色)名称作为附加参数。
附加的中间参数会在 $next 参数之后传递给中间件：
<?php
    namespace App\Http\Middleware;
    use Closure;
    class CheckRole
    {
        public function handle($request, Closure $next, $role)
        {
            if (! $request->user()->hasRole($role)) {
                // 重定向
            }
            return $next($request);
        }
    }


<?php
    namespace App\Http\Middleware;
    use Illuminate\Auth\Middleware\Authenticate as Middleware;
    class Authenticate extends Middleware
    {
        protected function redirectTo($request)
        {
            if (! $request->expectsJson()) {
                return route('login');
            }
        }
    }

## Terminable 中间件

有时可能需要在 HTTP 响应之后做一些工作。 
如果你在中间件上定义了一个 terminate 方法，并且你使用的是 FastCGI, 那么 terminate 方法会在响应发送到浏览器之后自动调用。


### CSRF 保护
Laravel 可以轻松使地保护你的应用程序免受 跨站请求伪造 (CSRF) 攻击。 
跨站点请求伪造是一种恶意攻击，它凭借已通过身份验证的用户身份来运行未经过授权的命令。
Laravel 会自动为每个活跃的用户的会话生成一个 CSRF「令牌」。该令牌用于验证经过身份验证的用户是否是向应用程序发出请求的用户。
无论何时，当您在应用程序中定义 HTML 表单时，都应该在表单中包含一个隐藏的 CSRF 标记字段，以便 CSRF 保护中间件可以验证该请求，
你可以使用 @csrf Blade 指令来生成令牌字段，如下：
    <form method="POST" action="/profile">
        @csrf
        ...
    </form>
包含在 web 中间件组里 VerifyCsrfToken 中间件会自动验证请求里的令牌是否与存储在会话中令牌匹配。
## CSRF 令牌 & JavaScript
当构建由 JavaScript 驱动的应用时，可以方便的让 JavaScript HTTP
函数库发起每一个请求时自动附上 CSRF 令牌。
默认情况下，resources/js/bootstrap.js 文件中提供的 Axios HTTP 库会使用 cookie 中加密的 XSRF-TOKEN 的值然后在请求时自动发送 X-XSRF-TOKEN 标头。 
如果不使用此库，则需要为应用程序手动配置此行为。
## CSRF 白名单
有时候你可能希望设置一组不需要的 CSRF 保护的 URL 。
例如，如果你正在使用 Stripe 处理付款并使用了他们的 webhook 系统，你会需要从 CSRF 的保护中排除 Stripe webhook 处理程序路由，
因为 Stripe 并不会给你的路由发送 CSRF 令牌。
典型做法，可以把这类路由放在 routes/web.php 外，因为 RouteServiceProvider 的 web 中间件适用于该文件中的所有路由。
也可以通过将这类 URL 添加到 VerifyCsrfToken 中间件的 $except 属性来排除对这类路由的 CSRF 保护
## X-CSRF-TOKEN
除了检查 POST 参数中的 CSRF 令牌外， VerifyCsrfToken 中间件还会检查 X-CSRF-TOKEN 请求头。你应该将令牌保存在 HTML meta 标签中，如下：
    <meta name="csrf-token" content="{{ csrf_token() }}">
然后，一旦你创建了 meta 标签，就可以指示像 jQuery 这样的库自动将令牌添加到所有请求的头信息中。还可以为基于 AJAX 的应用提供简单，方便的 CSRF 保护。如下：
$.ajaxSetup({
    headers: {
        'X-CSRF-TOKEN': $('meta[name="csrf-token"]').attr('content')
    }
});
## X-XSRF-TOKEN
Laravel 将当前的 CSRF 令牌存储在一个 XSRF-TOKEN cookie
中，该 cookie 包含在框架生成的每个响应中。你可以使用 cookie 值来设置 X-XSRF-TOKEN 请求头。
这个 cookie 主要是作为一种方便的方式发送的，因为一些 JavaScript 框架和库，例如 Angular 和 Axios ，会自动将它的值放入 X-XSRF-TOKEN 头中。
技巧：默认情况下，resources/js/bootstrap.js 文件包含的 Axios HTTP 库，会自动为你发送。

### 控制器

return view('articles.lists')->with('title',$title);
<h1><?php echo $title; ?></h1>
<h1>{{ $title }}</h1>

## {{  }}    {!!  !!}
# {{}}支持转义,一段html代码只是被当成普通的字符串输出,相当于 <?php echo htmlspecialchars($value); ?>
# {!! !!} 不支持转移,一段html代码可以被正常的解析,相当于 <?php echo $value; ?>

return view('articles.lists',['title'=>$title]);

return view('articles.lists',['title'=>$title,'introduction'=>$intro]);

public function index()
{
    $title = '<span style="color: red">文章</span>标题1';
    $intro = '文章一的简介';
    return view('articles.lists',compact('title','intro'));
}


#### HTTP 请求

### 接收请求
$name = $request->input('name');

Route::put('user/{id}', 'UserController@update');
public function update(Request $request, $id)
{
    //
}

$uri = $request->path();

$url = $request->url();  // 没有包含查询条件字符串

$url = $request->fullUrl();  // 包含查询条件字符串

$method = $request->method();

if ($request->isMethod('post')) {
    //
}

## PSR-7 请求
PSR-7 标准 指定了包括请求与响应在内的 HTTP 的消息接口。
如果你想要获取 PSR-7 请求实例而不是 Laravel 请求，那么你首先需要安装几个库。
Laravel 使用 Symfony HTTP Message Bridge 组件将典型的 Laravel 请求和响应转换为 PSR-7 的兼容实现：

## 获取输入

$input = $request->all();    // all 方法来获取 array 类型的全部输入数据

$input = $request->input();    // input 方法来获取全部输入的关联数组：

$name = $request->input('name');

$name = $request->input('name', 'Sally');  // 第二个参数传入一个默认值。这个值将会在当前请求不包含所需要的字段时返回

$name = $request->input('products.0.name');  // 当处理包含数组的表单时，可以使用 「.」 运算符来访问数组的数据

$names = $request->input('products.*.name');  // 当处理包含数组的表单时，可以使用 「.」 运算符来访问数组的数据

$query = $request->query();

$query = $request->query("name");

$query = $request->query("name","Helen");

$name = $request->name;  // 通过动态属性获取输入

$input = $request->only('username', 'password');

$input = $request->except(['credit_card']);

if ($request->has('name')) {
    //
}

if ($request->has(['name', 'email'])) {
    //
}

if ($request->hasAny(['name', 'email'])) {
    //
}

## 将输入数据闪存到 Session
Illuminate\Http\Request 类的 flash 方法可以把当前的输入闪存到 session，因此在用户向应用发起的下一次请求时它们仍然可用：

$request->flash();

$request->flashOnly(['username', 'email']);

$request->flashExcept('password');

## 闪存数据并跳转
如果你需要经常保存输入到 session 然后重定向到之前的页面，可以通过在跳转函数后链式调用 withInput 方法轻易地实现：:

return redirect('form')->withInput();

return redirect('form')->withInput(
    $request->except('password')
);

## 获取旧数据

若要获取上一次请求所保存的旧数据，可以在 Request 的实例上使用 old 方法。old 方法会从 [session] 取出之前被闪存的输入数据 (/docs/laravel/7.x/session)：

$username = $request->old('username');

<input type="text" name="username" value="{{ old('username') }}">

## Cookies


# 从请求中获取 Cookies

所有从 Laravel 框架创建的 cookies 都是加密的，并且使用授权码进行签名，这意味着如果它们被客户端改变就会失效。
若要从请求汇总获取 cookie，在 Illuminate\Http\Request 实例使用 cookie 方法即可：

$value = $request->cookie('name');

或者，你也可以使用 Cookie facade 来访问 cookie 值:

use Illuminate\Support\Facades\Cookie;
$value = Cookie::get('name');

# 将 Cookie 附加到响应中

你可以将一个 cookie 通过 cookie 方法附加到传出的 Illuminate\Http\Response 实例。
你需要传入名称、值、cookie 的过期时间（以分钟为单位）给该方法：

return response('Hello World')->cookie(
    'name', 'value', $minutes
);

cookie 同样也接受一些不太频繁使用的参数。通常而言，这些参数和 PHP 内置的 setcookie 方法有着相同的作用和意义：

return response('Hello World')->cookie(
    'name', 'value', $minutes, $path, $domain, $secure, $httpOnly
);

或者，你可以使用 Cookie facade 来 “排列” 用于从应用中附加到传出响应的 cookies。queue 方法接受一个 Cookie 实例或者用于创建 Cookie 实例的参数。
这些 cookie 将会在发送到浏览器之前被附加到传出响应：

Cookie::queue(Cookie::make('name', 'value', $minutes));

Cookie::queue('name', 'value', $minutes);

# 生成 Cookie 实例

如果你想要在生成一个将会被附加到响应实例的 Symfony\Component\HttpFoundation\Cookie 实例，你可以使用全局辅助函数 cookie。 
除非这个 cookie 被附加到响应实例，否则不会发送回客户：

$cookie = cookie('name', 'value', $minutes);

return response('Hello World')->cookie($cookie);

## 文件

# 获取上传的文件

你可以使用 file 方法或使用动态属性从 Illuminate\Http\Request 实例中访问上传的文件。 
该 file 方法返回 Illuminate\Http\UploadedFile 类的实例，该类继承了 PHP 的 SplFileInfo 类的同时也提供了各种与文件交互的方法：

$file = $request->file('photo');

$file = $request->photo;

当然你也可以使用 hasFile 方法判断请求中是否存在指定文件：

if ($request->hasFile('photo')) {
    //
}

# 验证成功上传

除了检查上传的文件是否存在外，你也可以通过 isValid 方法验证上传的文件是否有效：

if ($request->file('photo')->isValid()) {
    //
}

# 文件路径 & 扩展名

UploadedFile 类还包含访问文件的全路径和扩展名的方法。 extension 方法会根据文件内容判断文件的扩展名。该扩展名可能会和客户端提供的扩展名不同：

$path = $request->photo->path();

$extension = $request->photo->extension();

# 其它的文件方法

UploadedFile 实例上还有许多可用的方法。可以查看该类的 API 文档 了解这些方法的详细信息。

# 存储上传文件

要存储上传的文件，先配置好 文件系统。 
你可以使用 UploadedFile 的 store 方法把上传文件移动到你的某个磁盘上，该文件可能是本地文件系统中的一个位置，甚至像 Amazon S3 这样的云存储位置。

store 方法接受相对于文件系统配置的存储文件根目录的路径。这个路径不能包含文件名，因为系统会自动生成唯一的 ID 作为文件名。

store 方法还接受可选的第二个参数，用于存储文件的磁盘名称。这个方法会返回相对于磁盘根目录的文件路径：

$path = $request->photo->store('images');

$path = $request->photo->store('images', 's3');

如果你不想自动生成文件名，那么可以使用 storeAs 方法，它接受路径、文件名和磁盘名作为其参数：

$path = $request->photo->storeAs('images', 'filename.jpg');

$path = $request->photo->storeAs('images', 'filename.jpg', 's3');

## 配置可信代理
如果你的应用程序运行在失效的 TLS / SSL 证书的负载均衡器后，你可能会注意到你的应用程序有时不能生成 HTTPS 链接。
通常这是因为你的应用程序正在从端口 80 上的负载均衡器转发流量，却不知道是否应该生成安全链接。

解决这个问题需要在 Laravel 应用程序中包含 App\Http\Middleware\TrustProxies 中间件，这使得你可以快速自定义应用程序信任的负载均衡器或代理。
你的可信代理应该作为这个中间件的 $proxies 属性的数组列出。除了配置受信任的代理之外，还可以配置应该信任的代理 $header:

#### HTTP 响应

### 创建响应

## 字符串 & 数组

所有路由和控制器处理完业务逻辑之后都会返回一个发送到用户浏览器的响应，
Laravel 提供了多种不同的方式来返回响应，
最基本的响应就是从路由或控制器返回一个简单的字符串，
框架会自动将这个字符串转化为一个完整的 HTTP 响应

## Response 对象

通常，我们并不只是从路由动作简单返回字符串和数组，大多数情况下，都会返回一个完整的 Illuminate\Http\Response 实例或 视图。

返回完整的 Response 实例允许你自定义响应的 HTTP 状态码和响应头信息。 
Response 实例 继承自 Symfony\Component\HttpFoundation\Response 类， 该类提供了各种构建 HTTP 响应的方法：

Route::get('home', function () {
    return response('Hello World', 200)->header('Content-Type', 'text/plain');
});

## 添加响应头

大部分的响应方法都是可链式调用的，使得创建响应实例的过程更具可读性。例如，你可以在响应返回给用户前使用 header 方法为其添加一系列的头信息：

return response($content)
        ->header('Content-Type', $type)
        ->header('X-Header-One', 'Header Value')
        ->header('X-Header-Two', 'Header Value');

或者，你可以使用 withHeaders 方法来指定要添加到响应的头信息数组：

return response($content)->withHeaders([
            'Content-Type' => $type,
            'X-Header-One' => 'Header Value',
            'X-Header-Two' => 'Header Value',
        ]);

# 缓存控制中间件

Laravel 内置了一个 cache.headers 中间件，可以用来快速地为路由组设置 Cache-Control 头信息。
如果在指令集中声明了 etag，Laravel 会自动将 ETag 标识符设置为响应内容的 MD5 哈希值：

Route::middleware('cache.headers:public;max_age=2628000;etag')->group(function () {
    Route::get('privacy', function () {
        // ...
    });
    Route::get('terms', function () {
        // ...
    });
});

## 添加 Cookies 到响应

你可以使用响应上的 cookie 方法轻松地将为响应增加 Cookies。

例如，你可以像这样使用 cookie 方法生成一个 cookie 并轻松地将其附加到响应上：

return response($content)->header('Content-Type', $type)->cookie('name', 'value', $minutes);

cookie 方法还接受一些不太频繁使用的参数。通常，这些参数与原生 PHP 的 setcookie 方法的参数有着相同的目的和含义：

->cookie($name, $value, $minutes, $path, $domain, $secure, $httpOnly)

或者，你可以使用 Cookie facade 「队列」， Cookie 以附加到应用程序的传出响应。 
queue 方法接受一个 Cookie 实例或创建 Cookie 实例所需的参数。 这些 cookie 在发送到浏览器之前会附加到传出响应中：

Cookie::queue(Cookie::make('name', 'value', $minutes));

Cookie::queue('name', 'value', $minutes);

## Cookies & 加密

默认情况下，Laravel 生成的所有 Cookie 都是经过加密和签名，因此不能被客户端修改或读取。 
如果你想要应用程序生成的部分 Cookie 不被加密，
那么可以使用在 app/Http/Middleware 目录中 App\Http\Middleware\EncryptCookies 中间件的 $except 属性：

## 重定向

# return redirect('home/dashboard');
# return back()->withInput();
# return redirect()->route('login');   // 重定向到命名路由
# return redirect()->route('profile', ['id' => 1]);
# return redirect()->action('HomeController@index');
# return redirect()->away('https://www.google.com');


重定向响应是 Illuminate\Http\RedirectResponse 类的实例，并且包含用户需要重定向至另一个 URL 所需的头信息。
Laravel 提供了几种方法用于生成 RedirectResponse 实例。其中最简单的方法是使用全局辅助函数 redirect：

Route::get('dashboard', function () {
    return redirect('home/dashboard');
});

有时候你可能希望将用户重定向到之前的位置，比如提交的表单无效时。
这时你可以使用全局辅助函数 back 来执行此操作。
由于这个功能利用了 会话控制，请确保调用 back 函数的路由使用 web 中间件组或所有 Session 中间件：

Route::post('user/profile', function () {
    // 验证请求
    return back()->withInput();
});

## 重定向到控制器行为

还可以生成到 controller action 的重定向。
要达到这个目的，只要把 控制器 和 action 的名称传递给 action 方法。
记住，不需要传递控制器的全部命名空间，Laravel 的 RouteServiceProvider 会自动将其设置为基本控制器的命名空间：

return redirect()->action('HomeController@index');

如果控制器路由需要参数，可以将其作为 action 方法的第二个参数：

return redirect()->action(
    'UserController@profile', ['id' => 1]
);

## 重定向到外部域名

有时候你需要重定向到应用外的域名。
调用 away 方法可以达到此目的，它会创建一个不带有任何额外的 URL 编码、有效性校验和检查的 RedirectResponse 实例：

return redirect()->away('https://www.google.com');

## 重定向并使用闪存的 Session 数据

重定向到新的 URL 的同时 传送数据给 session 是很常见的。 
通常会在成功执行一个动作并传送消息给 session 之后这样做。
为了方便起见，你可以创建一个 RedirectResponse 实例并在链式方法调用中将数据传送给 session ：

Route::post('user/profile', function () {
    // 更新用户的个人资料...
    return redirect('dashboard')->with('status', 'Profile updated!');
});

在用户重定向后，可以显示 session 中的传送数据。比如使用 Blade syntax ：

@if (session('status'))
    <div class="alert alert-success">
        {{ session('status') }}
    </div>
@endif

## 视图响应

如果需要把 视图 作为响应内容返回的同时，控制响应状态和头信息，就需要调用 view 方法：

return response()->view('hello', $data, 200)->header('Content-Type', $type);

如果不需要传递自定义的 HTTP 状态码和自定义头信息，还可以使用全局的 view 辅助函数。

## JSON 响应

json 自动将 Content-Type 头信息设置为 application/json，同时使用 PHP 的 json_encode 函数将给定的数组转换为 JSON ：

return response()->json([
    'name' => 'Abigail',
    'state' => 'CA'
]);

如果想要创建 JSONP 响应，可以结合 withCallback 方法使用 json 方法：

return response()
            ->json(['name' => 'Abigail', 'state' => 'CA'])
            ->withCallback($request->input('callback'));

## 文件下载#

download 方法可以用于生成强制用户浏览器下载给定路径文件的响应。 
download 方法文件名作为其第二个参数，它将作为用户下载文件的文件名。最后，你可以传递 HTTP 头信息数组作为其第三个参数：

return response()->download($pathToFile);

return response()->download($pathToFile, $name, $headers);

return response()->download($pathToFile)->deleteFileAfterSend();

{注意} 用于管理文件下载的 Symfony HttpFoundation 要求下载的文件有一个 ASCII 文件名。

## 流下载

有时，你可能希望将给定操作的字符串响应转换为下载响应，而不需要将其写入磁盘。
此时可以使用 streamDownload 方法。这个方法接受回调、文件名和可选的头信息数组作为参数：

return response()->streamDownload(function () {
    echo GitHub::api('repo')
                ->contents()
                ->readme('laravel', 'laravel')['contents'];
}, 'laravel-readme.md');

## 文件响应

file 方法用于直接在用户浏览器显示一个图片或 PDF 之类的文件，而不是下载。
这个方法接受文件路径作为第一个参数，头信息数组作为第二个参数：

return response()->file($pathToFile);

return response()->file($pathToFile, $headers);

## 响应宏

如果你想要定义一个自定义的可以在多个路由和控制器中复用的响应，可以使用 Response 门面上的 macro 方法。

#### 视图

## 与所有视图共享数据

有时候，你可能需要共享一段数据给应用程序的所有视图。 
你可以在服务提供器的 boot 方法中调用视图门面（Facade）的 share 方法。
例如，可以将它们添加到 AppServiceProvider 或者为它们生成一个单独的服务提供器：

#### URL

echo url("/posts/{$post->id}");

echo url()->current();

echo url()->full();

echo url()->previous();

use Illuminate\Support\Facades\URL;
echo URL::current();

## 命名路由的 URL

辅助函数 route 可以用于为指定路由生成 URL。
命名路由生成的 URL 不与路由上定义的 URL 相耦合。
因此，就算路由的 URL 有任何改变，都不需要对 route 函数调用进行任何更改。
例如，假设你的应用程序包含以下路由：

Route::get('/post/{post}', function () {
    //
})->name('post.show');

#### SESSION

$value = $request->session()->get('key');
$data = $request -> session() -> all();   // 获取所有的session；
$request -> session() -> has("user");     // 判断某个session是否存在  has / exists
$request -> session() -> put('key','value');   // 通过实例存储session
$request->session()->push('user.teams', 'developers');    // 在 Session 数组中保存数据
$value = $request->session()->pull('key', 'default');   // 检索并删除
session(['key'=>'value']);   // 通过全局辅助函数存储session
$request->session()->forget('key');     // 删除单个值...
$request->session()->forget(['key1', 'key2']);      // 删除多个值...

## 配置

Session 的配置文件存储在 config/session.php 文件中。
请务必查看此文件中对于你而言可用的选项。
默认情况下，Laravel 为绝大多数应用程序配置的 Session 驱动为 file 。
在生产环境中，你可以考虑使用 memcached 或 redis 驱动，让 Session 的性能更加出色。

Session driver 的配置预设了每个请求存储 Session 数据的位置。Laravel 自带了几个不错而且开箱即用的驱动：

file - 将 Session 存储在 storage/framework/sessions 中。
cookie - Sessions 被存储在安全加密的 cookie 中。
database - Sessions 被存储在关系型数据库中。
memcached / redis - Sessions 被存储在基于高速缓存的存储系统中。
array - Sessions 存储在 PHP 数组中，但不会被持久化。

#### 表单验证

$request->validate([
    'title' => 'required|unique:posts|max:255',
    'author.name' => 'required',
    'author.description' => 'required',
]);



<!-- /resources/views/post/create.blade.php -->

<h1>Create Post</h1>

@if ($errors->any())
    <div class="alert alert-danger">
        <ul>
            @foreach ($errors->all() as $error)
                <li>{{ $error }}</li>
            @endforeach
        </ul>
    </div>
@endif

<!-- Create Post Form -->




















### Blade 模板

Blade 是 Laravel 提供的一个简单而又强大的模板引擎。
和其他流行的 PHP 模板引擎不同，Blade 并不限制你在视图中使用原生 PHP 代码。
所有 Blade 视图文件都将被编译成原生的 PHP 代码并缓存起来，除非它被修改，否则不会重新编译，这就意味着 Blade 基本上不会给你的应用增加任何负担。
Blade 视图文件使用 .blade.php 作为文件扩展名，被存放在 resources/views 目录。

### 模板继承

## 定义布局

# Blade 的两个主要优点是 模板继承和区块

<!-- 位于 resources/views/layouts/app.blade.php -->

<html>
    <head>
        <title>App Name - @yield('title')</title>
    </head>
    <body>
        @section('sidebar')
            This is the master sidebar.
        @show

        <div class="container">
            @yield('content')
        </div>
    </body>
</html>

@section 指令定义了视图的一部分内容， @yield 指令是用来显示指定部分的内容。

<!-- 位于 resources/views/child.blade.php -->

@extends('layouts.app')
@section('title', 'Page Title')
@section('sidebar')
    @parent
    <p>This is appended to the master sidebar.</p>
@endsection
@section('content')
    <p>This is my body content.</p>
@endsection

sidebar 片段利用 @parent 指令向布局的 sidebar 追加（而非覆盖）内容。 在渲染视图时，@parent 指令将被布局中的内容替换。







#### 用户认证
提示： 想要快速开始吗？ Composer 安装 laravel/ui 包并在一个全新的 Laravel 应用程序中运行 php artisan ui vue --auth 。
迁移数据库后，将浏览器导航到 http://your-app.test/register 或分配给应用程序的任何其他 URL。这两个命令将负责构建整个认证系统！



#### artisan 命令行

php artisan list    // 查看所有可用的 Artisan 命令


#### 缓存系统

Laravel 为各种后端缓存提供了丰富而统一的 API，其配置信息位于 config/cache.php 文件中。
在该文件中你可以指定应用默认使用哪个缓存驱动。
Laravel 支持当前流行的后端缓存，例如 Memcached 和 Redis 。

缓存配置文件还包含各种其他选项，这些选项都记录在文件中，因此请确保阅读这些选项。
默认情况下，Laravel 配置为使用 file 缓存驱动，它将序列化的缓存对象存储在文件系统中。
对于较大型应用，建议使用更强大的驱动程序，例如 Memcached 或 Redis。
你甚至可以为同一个驱动程序配置多个缓存配置。

### 驱动的前提条件#

## 数据库

当使用 database 缓存驱动时，你需要配置一个表来存放缓存数据。下面是构建缓存数据表结构的 Schema 声明

可以使用 Artisan 命令 php artisan cache:table 来生成合适的迁移

Schema::create('cache', function ($table) {
    $table->string('key')->unique();
    $table->text('value');
    $table->integer('expiration');
});

## Memcached

使用 Memcached 驱动需要安装 Memcached PECL 扩展包 。

## Redis

在使用 Laravel 的 Redis 缓存之前，你需要通过 PECL 安装 PhpRedis PHP 扩展，或者通过 Composer 安装 predis/predis 包（~1.0）。

### 缓存的使用  Cache:put()  Cache:pull()  Cache:get()  Cache:has()  Cache:increment()  Cache:decrement()  

$value = Cache::get('key');

## 访问多个缓存存储

使用 Cache Facade，你可以通过 store 方法来访问各种缓存存储。
传入 store 方法的键应该对应 cache 配置信息文件中的 stores 配置数组中所列出的一个：

$value = Cache::store('file')->get('foo');

Cache::store('redis')->put('bar', 'baz', 600); // 10 分钟

## 从缓存中获取数据

Cache Facade 的 get 方法用于从缓存中获取数据。如果该数据在缓存中不存在，那么该方法将返回 null 。
正如你想的那样，你也可以向 get 方法传递第二个参数，用来指定如果查找的数据不存在时你希望返回的默认值：

$value = Cache::get('key');

$value = Cache::get('key', 'default');

你甚至可以传递一个 Closure 作为默认值。如果指定的数据在缓存中不存在，将返回 Closure 的结果。
传递闭包的方法允许你从数据库或其他外部服务中获取默认值

$value = Cache::get('key', function () {
    return DB::table(...)->get();
});

## 检查缓存项是否存在

has 方法可以用于判断缓存项是否存在。如果值为 null，则该方法将会返回 false ：

if (Cache::has('key')) {
    //
}

## 递增与递减值

increment 和 decrement 方法可以用来调整缓存中整数项的值。这两个方法都可以传入第二个可选参数，这个参数用来指明要递增或递减的数量：

Cache::increment('key');
Cache::increment('key', $amount);
Cache::decrement('key');
Cache::decrement('key', $amount);

## 获取和存储

有时你可能想从缓存中获取一个数据，而当请求的缓存项不存在时，程序能为你存储一个默认值。
例如，你可能想从缓存中获取所有用户，当缓存中不存在这些用户时，程序将从数据库将这些用户取出并放入缓存。你可以使用 Cache::remember 方法来实现：

$value = Cache::remember('users', $seconds, function () {
    return DB::table('users')->get();
});

如果缓存中不存在你想要的数据时，则传递给 remember 方法的 闭包 将被执行，然后将其结果返回并放置到缓存中。

你可以使用 rememberForever 方法从缓存中获取数据或者永久存储它：

$value = Cache::rememberForever('users', function () {
    return DB::table('users')->get();
});

## 获取和删除  Cache:pull()

如果你需要从缓存中获取到数据之后再删除它，你可以使用 pull 方法。和 get 方法一样，如果缓存不存在，则返回 null ：

$value = Cache::pull('key');

## 在缓存中存储数据#   Cache:put()

你可以使用 Cache Facade 的 put 方法将数据存储到缓存中：

Cache::put('key', 'value', $seconds);

如果缓存的过期时间没有传递给 put 方法， 则缓存将永久有效：

Cache::put('key', 'value');

除了以整数形式传递过期时间的秒数，你还可以传递一个 DateTime 实例来表示该数据的到期时间：

Cache::put('key', 'value', now()->addMinutes(10));

## 只存储没有的数据  Cache:add()

add 方法将只存储缓存中不存在的数据。如果存储成功，将返回 true ，否则返回 false ：

Cache::add('key', 'value', $seconds);

## 数据永久存储  Cache:forever()

forever 方法可用于持久化将数据存储到缓存中。因为这些数据不会过期，所以必须通过 forget 方法从缓存中手动删除它们：

Cache::forever('key', 'value');

提示：如果你使用 Memcached 驱动，当缓存数据达到存储上限时，「永久存储」 的数据可能会被删除。

## 从缓存中删除数据  Cache:forget()  Cache:put()  Cache:flush()

你可以使用 forget 方法从缓存中删除这些数据：

Cache::forget('key');

你也可以通过提供零或者负的 TTL 值来删除这些数据：

Cache::put('key', 'value', 0);

Cache::put('key', 'value', -5);

你可以使用 flush 方法清空所有的缓存：

Cache::flush();

注意：清空缓存的方法并不会考虑缓存前缀，会将缓存中的所有内容删除。因此在清除与其它应用程序共享的缓存时，请慎重考虑。

### 原子锁#

注意：要想使用该特性，你的应用必须使用 memcached，dynamodb 或 redis 缓存驱动作为你应用的默认缓存驱动。
此外，所有服务器必须与同一中央缓存服务器进行通信。















#### 数据库

### 查询构造器

$users = DB::table('users')->get();    // get() 获取所有行
foreach($users as $user){
    echo $user -> name;
}

$user = DB::table('users')->where('name', 'John')->first();  // first() 获取单行数据

$email = DB::table('users')->where('name', 'John')->value('email');   // value() 获取单个值

$user = DB::table('users')->find(3);   // find() 通过id获取单行数据

$titles = DB::table('roles')->pluck('title');  // pluck() 获取单列值
foreach($titles as $title){
    echo $title;
}

$roles = DB::table('users')->pluck('title','name');  // pluck('title','name') 将roles表中的name字段当做键名,title字段当做键值返回
foreach($roles as $name => $title){
    echo $title;
}

## 分块结果
如果你需要处理上千条数据库记录，你可以考虑使用 chunk 方法。该方法一次获取结果集的一小块，并将其传递给 闭包 函数进行处理。
该方法在 Artisan 命令 编写数千条处理数据的时候非常有用;

DB::table('users')->orderBy('id')->chunk(100,function($users){
    foreach($users as $user){
        
    }
})

# 你可以通过在 闭包 中返回 false 来终止继续获取分块结果：

DB::table('users')->orderBy('id')->chunk(100, function ($users) {
    // Process the records...

    return false;
});

# 如果要在分块结果时更新数据库记录，则块结果可能会和预计的返回结果不一致。 因此，在分块更新记录时，最好使用 chunkById 方法。 此方法将根据记录的主键自动对结果进行分页：

DB::table('users')->where('active', false)
    ->chunkById(100, function ($users) {
        foreach ($users as $user) {
            DB::table('users')
                ->where('id', $user->id)
                ->update(['active' => true]);
        }
    });

## 聚合

查询构造器还提供了各种聚合方法，比如 count, max，min， avg，还有 sum。你可以在构造查询后调用任何方法：

$users = DB::table('users')->count();

$price = DB::table('orders')->max('price');

## 判断记录是否存在

除了通过 count 方法可以确定查询条件的结果是否存在之外，还可以使用 exists 和 doesntExist 方法：

return DB::table('orders')->where('finalized', 1)->exists();

return DB::table('orders')->where('finalized', 1)->doesntExist();



$users = DB::table('users')->select('name', 'email as user_email')->get();  // select() 指定输出列

$users = DB::table('users')->distinct()->get();  // distinct() 输出结果不重复

如果你已经有了一个查询构造器实例，并且希望在现有的查询语句中加入一个字段，那么你可以使用 addSelect 方法：

$query = DB::table('users')->select('name');

$users = $query->addSelect('age')->get();

### Joins

## Inner Join 语句

查询构造器也可以编写 join 方法。
若要执行基本的「内链接」，你可以在查询构造器实例上使用 join 方法。
传递给 join 方法的第一个参数是你需要连接的表的名称，而其他参数则使用指定连接的字段约束。你还可以在单个查询中连接多个数据表：

$users = DB::table('users')
            ->join('contacts', 'users.id', '=', 'contacts.user_id')
            ->join('orders', 'users.id', '=', 'orders.user_id')
            ->select('users.*', 'contacts.phone', 'orders.price')
            ->get();

## Left Join / Right Join 语句

如果你想使用 「左连接」或者 「右连接」代替「内连接」 ，可以使用 leftJoin 或者 rightJoin 方法。这两个方法与 join 方法用法相同：

$users = DB::table('users')->leftJoin('posts', 'users.id', '=', 'posts.user_id')->get();

$users = DB::table('users')->rightJoin('posts', 'users.id', '=', 'posts.user_id')->get();

## Cross Join 语句

使用 crossJoin 方法和你想要连接的表名做 「交叉连接」。交叉连接在第一个表和被连接的表之间会生成笛卡尔积：

$users = DB::table('sizes')->crossJoin('colors')->get();

## 高级 Join 语句

你可以指定更高级的 join 语句。比如传递一个 闭包 作为 join 方法的第二个参数。此 闭包 接收一个 JoinClause 对象，从而指定 join 语句中指定的约束：

DB::table('users')->join('contacts', function ($join) {
        $join->on('users.id', '=', 'contacts.user_id')->orOn(...);
    })->get();

如果你想要在连接上使用「where」 风格的语句，你可以在连接上使用 where 和 orWhere 方法。这些方法会将列和值进行比较，而不是列和列进行比较：

DB::table('users')->join('contacts', function ($join) {
        ->where('contacts.user_id', '>', 5);
    })->get();

## 子连接查询

你可以使用 joinSub，leftJoinSub 和 rightJoinSub 方法关联一个查询作为子查询。他们每一种方法都会接收三个参数：子查询，表别名和定义关联字段的闭包：

$latestPosts = DB::table('posts')
    ->select('user_id', DB::raw('MAX(created_at) as last_post_created_at'))
    ->where('is_published', true)
    ->groupBy('user_id');

$users = DB::table('users')
        ->joinSub($latestPosts, 'latest_posts', function ($join) {
            $join->on('users.id', '=', 'latest_posts.user_id');
        })->get();

## Unions

查询构造器还提供了将两个查询 「联合」 的快捷方式。比如，你可以先创建一个查询，然后使用 union 方法将其和第二个查询进行联合：

$first = DB::table('users')->whereNull('first_name');
$users = DB::table('users')->whereNull('last_name')->union($first)->get();

## Where 语句  >    <    >=    <=    <>    like

$users = DB::table('users')->where('votes', '=', 100)->get();

$users = DB::table('users')->where('name', 'like', 'T%')->get();

$users = DB::table('users')->where([
        ['status', '=', '1'],
        ['subscribed', '<>', '1'],
    ])->get();





## orderBy     asc/desc

orderBy 方法允许你通过给定字段对结果集进行排序。 orderBy 的第一个参数应该是你希望排序的字段，第二个参数控制排序的方向，可以是 asc 或 desc：

$users = DB::table('users')->orderBy('name', 'desc')->get();

## latest / oldest

latest 和 oldest 方法可以使你轻松地通过日期排序。它默认使用 created_at 列作为排序依据。当然，你也可以传递自定义的列名：

$user = DB::table('users')->latest()->first();

## inRandomOrder

inRandomOrder 方法被用来将结果随机排序。例如，你可以使用此方法随机找到一个用户。

$randomUser = DB::table('users')->inRandomOrder()->first();

## groupBy / having

groupBy 和 having 方法可以将结果分组。 having 方法的使用与 where 方法十分相似：

$users = DB::table('users')->groupBy('account_id')->having('account_id', '>', 100)->get();

你可以向 groupBy 方法传递多个参数：

$users = DB::table('users')->groupBy('first_name', 'status')->having('account_id', '>', 100)->get();

## skip / take    offset / limit

$users = DB::table('users')->skip(10)->take(5)->get();

或者你也可以使用 limit 和 offset 方法：

$users = DB::table('users')->offset(10)->limit(5)->get();

## 条件语句 wher

## 插入 insert

查询构造器还提供了 insert 方法用于插入记录到数据库中。 insert 方法接收数组形式的字段名和字段值进行插入操作：

DB::table('users')->insert(
    ['email' => 'john@example.com', 'votes' => 0]
);

你甚至可以将数组传递给 insert 方法，将多个记录插入到表中：

DB::table('users')->insert([
    ['email' => 'taylor@example.com', 'votes' => 0],
    ['email' => 'dayle@example.com', 'votes' => 0]
]);

insertOrIgnore 方法用于忽略重复插入记录到数据库的错误：

DB::table('users')->insertOrIgnore([
    ['id' => 1, 'email' => 'taylor@example.com'],
    ['id' => 2, 'email' => 'dayle@example.com']
]);

## 自增 ID  insertGetId

如果数据表有自增 ID , 使用 insertGetId 方法来插入记录并返回 ID 值

$id = DB::table('users')->insertGetId(['email' => 'john@example.com', 'votes' => 0]);

## 更新 update

$affected = DB::table('users')->where('id', 1)->update(['votes' => 1]);

## 更新或新增

updateOrInsert 方法将首先尝试使用第一个参数的键和值对来查找匹配的数据库记录。 
如果记录存在，则使用第二个参数中的值去更新记录。 如果找不到记录，将插入一个新记录，更新的数据是两个数组的集合：

DB::table('users')->updateOrInsert(['email' => 'john@example.com', 'name' => 'John'],['votes' => '2']);

## 更新 JSON 字段

## 自增 & 自减 increment decrement

查询构造器还为给定字段的递增或递减提供了方便的方法。此方法提供了一个比手动编写 update 语句更具表达力且更精练的接口。

这两种方法都至少接收一个参数：需要修改的列。第二个参数是可选的，用于控制列递增或递减的量：

DB::table('users')->increment('votes');

DB::table('users')->increment('votes', 5);

DB::table('users')->decrement('votes');

DB::table('users')->decrement('votes', 5);

你也可以在操作过程中指定要更新的字段：

DB::table('users')->increment('votes', 1, ['name' => 'John']);

## 删除

查询构造器也可以使用 delete 方法从表中删除记录。 在使用 delete 前，可以添加 where 子句来约束 delete 语法：

DB::table('users')->delete();

DB::table('users')->where('votes', '>', 100)->delete();

# 如果你需要清空表，你可以使用 truncate 方法，它将删除所有行，并重置自增 ID 为零：

DB::table('users')->truncate();

## 悲观锁

查询构造器也包含一些可以帮助你在 select 语法上实现「悲观锁定」的函数。
若想在查询中实现一个「共享锁」， 你可以使用 sharedLock 方法。 共享锁可防止选中的数据列被篡改，直到事务被提交为止:

DB::table('users')->where('votes', '>', 100)->sharedLock()->get();

或者，你可以使用 lockForUpdate 方法。使用 「update」锁可避免行被其它共享锁修改或选取：

DB::table('users')->where('votes', '>', 100)->lockForUpdate()->get();

## 调试

你可以使用 dd 或者 dump 方法输出查询结果或者 SQL 语句。 
dd 方法可以显示调试信息，然后停止执行请求。 
dump 方法同样可以显示调试信息，但是不会停止执行请求：

DB::table('users')->where('votes', '>', 100)->dd();

DB::table('users')->where('votes', '>', 100)->dump();

### 分页  Laravel 的分页器将 查询构造器 和 Eloquent ORM 结合起来

$users = DB::table('users')->paginate(15);
return view('user.index', ['users' => $users]);

<div class="container">
    @foreach ($users as $user)
        {{ $user->name }}
    @endforeach
</div>
{{ $users->links() }}

### 数据库迁移
laravel版本: php artisan --version

## 生成迁移 php artisan make:migration create_goods_table

# 或者 php artisan make:migration create_news_table --create=news
php artisan migrate 
php artisan make:migration add_votes_to_goods_table --table=goods

## 重置APP_KEY  php artisan key:generate

# php artisan list
up : 添加 和 修改
down : 删除

php artisan migrate:rollback

    创建表：
        php artisan make:migration create_tableName_table
        php artisan migrate
    修改表：
    删除表：


#### Eloquent ORM

### Eloquent：入门

Laravel 的 Eloquent ORM 提供了一个漂亮、简洁的 ActiveRecord 实现来和数据库交互。
每个数据库表都有一个对应的「模型」用来与该表交互。

## 模型定义

模型通常在 app 目录中，但你可以根据 composer.json 文件将他们放置在可以被自动加载的任意位置。
所有的 Eloquent 模型都继承至 Illuminate\Database\Eloquent\Model 类。

创建模型最简单的方法就是使用 make:model Artisan 命令:php artisan make:model Flight

如果要在生成模型的时候生成 数据库迁移 ，可以使用 --migration 或 -m 选项：

php artisan make:model Flight --migration

php artisan make:model Flight -m












## If 语句

你可以使用 @if, @elseif, @else, 和 @endif 指令来构造 if 语句。这些指令的功能与它们在 PHP 中对应的语句功能相同：

@if (count($records) === 1)
    我有一条记录！
@elseif (count($records) > 1)
    我有好多条记录！
@else
    我没有记录！
@endif

## 除了已经讨论过的条件指令之外， @isset 和 @empty 指令还可以用作各自 PHP 函数的快捷方式：

@isset($records)
    // 变量 $records 已定义且不为空...
@endisset

@empty($records)
    // 变量 $records 为空...
@endempty

## Switch 语句

Switch 语句可以使用 @switch, @case, @break, @default 和 @endswitch 指令来构造：

@switch($i)
    @case(1)
        First case...
        @break

    @case(2)
        Second case...
        @break

    @default
        Default case...
@endswitch

## 循环#

除了条件语句外，Blade 还提供了用于处理 PHP 循环结构的简单指令。同样，这些指令中的每个函数的功能都与对应的 PHP 的函数功能相同：

@for ($i = 0; $i < 10; $i++)
    The current value is {{ $i }}
@endfor

@foreach ($users as $user)
    <p>This is user {{ $user->id }}</p>
@endforeach

@forelse ($users as $user)
    <li>{{ $user->name }}</li>
@empty
    <p>No users</p>
@endforelse

@while (true)
    <p>I'm looping forever.</p>
@endwhile







### Redis 开源的 高级键值对存储数据库 包含字符串、哈希、列表、集合和有序集合  数据结构数据库
Redis 是一个开源的，高级键值对存储数据库。
它包含 字符串，哈希，列表，集合，和 有序集合 这些数据类型，所以它通常被称为数据结构服务器。
在将 Redis 与 Laravel 一起使用前，鼓励你通过 PECL 安装并使用 PhpRedis PHP 扩展。
尽管扩展安装起来更复杂，但对于大量使用 Redis 的应用程序可能会产生更好的性能。
也可以通过 Composer 安装 predis/predis 包：
composer require predis/predis












### artisan

zhangmenglei@zhangmengleideMacBook-Pro-2 laravel_shop % php artisan list
Laravel Framework 7.26.1

Usage:
command [options] [arguments]

Options:
-h, --help            Display this help message
-q, --quiet           Do not output any message
-V, --version         Display this application version
    --ansi            Force ANSI output
    --no-ansi         Disable ANSI output
-n, --no-interaction  Do not ask any interactive question
    --env[=ENV]       The environment the command should run under
-v|vv|vvv, --verbose  Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug

Available commands:
clear-compiled       Remove the compiled class file
down                 Put the application into maintenance mode
env                  Display the current framework environment
help                 Displays help for a command
inspire              Display an inspiring quote
list                 Lists commands
migrate              Run the database migrations
optimize             Cache the framework bootstrap files
serve                Serve the application on the PHP development server
test                 Run the application tests
tinker               Interact with your application
up                   Bring the application out of maintenance mode
## auth
auth:clear-resets    Flush expired password reset tokens
## cache
cache:clear          Flush the application cache
cache:forget         Remove an item from the cache
cache:table          Create a migration for the cache database table
## config
config:cache         Create a cache file for faster configuration loading
config:clear         Remove the configuration cache file
## db
db:seed              Seed the database with records
db:wipe              Drop all tables, views, and types
## event
event:cache          Discover and cache the application's events and listeners
event:clear          Clear all cached events and listeners
event:generate       Generate the missing events and listeners based on registration
event:list           List the application's events and listeners
## key
key:generate         Set the application key
## make
make:cast            Create a new custom Eloquent cast class
make:channel         Create a new channel class
make:command         Create a new Artisan command
make:component       Create a new view component class
make:controller      Create a new controller class
make:event           Create a new event class
make:exception       Create a new custom exception class
make:factory         Create a new model factory
make:job             Create a new job class
make:listener        Create a new event listener class
make:mail            Create a new email class
make:middleware      Create a new middleware class
make:migration       Create a new migration file
make:model           Create a new Eloquent model class
make:notification    Create a new notification class
make:observer        Create a new observer class
make:policy          Create a new policy class
make:provider        Create a new service provider class
make:request         Create a new form request class
make:resource        Create a new resource
make:rule            Create a new validation rule
make:seeder          Create a new seeder class
make:test            Create a new test class
## migrate
migrate:fresh        Drop all tables and re-run all migrations
migrate:install      Create the migration repository
migrate:refresh      Reset and re-run all migrations
migrate:reset        Rollback all database migrations
migrate:rollback     Rollback the last database migration
migrate:status       Show the status of each migration
notifications
notifications:table  Create a migration for the notifications table
## optimize
optimize:clear       Remove the cached bootstrap files
## package
package:discover     Rebuild the cached package manifest
## queue
queue:failed         List all of the failed queue jobs
queue:failed-table   Create a migration for the failed queue jobs database table
queue:flush          Flush all of the failed queue jobs
queue:forget         Delete a failed queue job
queue:listen         Listen to a given queue
queue:restart        Restart queue worker daemons after their current job
queue:retry          Retry a failed queue job
queue:table          Create a migration for the queue jobs database table
queue:work           Start processing jobs on the queue as a daemon
## route
route:cache          Create a route cache file for faster route registration
route:clear          Remove the route cache file
route:list           List all registered routes
## schedule
schedule:run         Run the scheduled commands
## session
session:table        Create a migration for the session database table
## storage
storage:link         Create the symbolic links configured for the application
## stub
stub:publish         Publish all stubs that are available for customization
## vendor
vendor:publish       Publish any publishable assets from vendor packages
## view
view:cache           Compile all of the application's Blade templates
view:clear           Clear all compiled view files