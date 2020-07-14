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