1、代码所在的文件夹加权限；
2、除了静态资源文件，其余都要加上只读权限；静态资源文件加上只读只写权限；
3、图片最好用二进制流的方式储存；
4、上传文件的地方加上只写权限；最好用伪静态去写；生成的文件也加上只读权限；
5、代码进行加密处理，就是代码以乱码的形式展示出来；
6、数据最好用InnoDB引擎；
7、可以使用存储过程进行数据加密；
8、传输过程中的伪检测；
9、在服务器已知的漏洞打上补丁；
10、端口不要随便外放；

PHP可以用goto进行加密