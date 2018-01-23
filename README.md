# php-file
 PHP文件系统处理



                  所有文件处理都是使用系统函数完成的。
                  是基于Linux/Unix系统为模型

                  文件系统处理的作用：
                    1. 所有的项目离不开文件处理
                    2. 可以用文件长时间保存数据
                    3. 建立缓存， 服务器中文件操作

                  文件处理
                  1. 文件类型
                    以Linux为模型的， 在Windows只能获取file, dir或unknow 三种类型
                    在Linux/Unix下， block, char, dir, fifo, file, link, unknown和种型
                    block :块设置文件，磁盘分区，软驱， cd-rom等
                    char: 字符设备，I/O 以字符为单位， 键盘，打印机等
                    dir: 目录也是文件的一种
                    fifo: 
                    file:
                    link: 
                    unknown	

                      filetype("目录或文件名")

                      is_array();
                      is_int();
                      is_string();
                      is_null;
                      is_bool();

                  is_dir -- 判断给定文件名是否是一个目录
                  is_executable -- 判断给定文件名是否可执行
                  is_file -- 判断给定文件名是否为一个正常的文件
                  is_link -- 判断给定文件名是否为一个符号连接
                  is_readable -- 判断给定文件名是否可读
                  is_uploaded_file -- 判断文件是否是通过 HTTP POST 上传的
                  is_writable -- 判断给定的文件名是否可写
                  is_writeable -- is_writable() 的别名


                  2. 文件的属性
                    file_exists();  检查文件或目录是否存在
                    filesize();     取得文件大小
                    is_readable();   判断给定文件名是否可读
                    is_writeable();
                    filectime();     取得文件的 inode 修改时间
                    filemtime();      取得文件修改时间
                    fileatime ();    取得文件的上次访问时间
                    stat();           给出文件的信息
                    
                    
                     
             例子      file_exists();  检查文件或目录是否存在        
                    
                        if(is_writable("demo.txt")){
                            echo "这是一个目录";
                          }else{
                            echo "这是一个文件";
                          }
                          
                          输出  这是一个文件
                    
                    
                    
             设定用于一个脚本中所有日期时间函数的默认时区（这里设置为中国）
              date_default_timezone_set("PRC");

                function getFilePro($fileName){
                  if(!file_exists($fileName)){
                    echo "文件或目录{$fileName} 不存在<br>";
                    return;
                  }else{
                    echo "文件的类型".filetype($fileName)."<br>";
                  }	

                  if(is_file($fileName)){
                    echo "这是一个文件<br>";
                    echo "文件的大小为".getFileSize(filesize($fileName))."<br>";
                  }

                  if(is_dir($fileName)){
                    echo "这是一个目录<br>";
                  }

                  if(is_readable($fileName)){
                    echo "这个文件可以读<br>";
                  }
                  if(is_writable($fileName)){
                    echo "这个文件可以写<br>";
                  }
                  if(is_executable($fileName)){
                    echo "这个文件可以执行<br>";
                  }

                  echo "文件的创建时间：".date("Y-m-d H:i:s",filectime($fileName))."<br>";
                  echo "文件的修改时间：".date("Y-m-d H:i:s",filemtime($fileName))."<br>";
                  echo "文件的最后访问时间：".date("Y-m-d H:i:s",fileatime($fileName))."<br>";

                }

            这是最常用的给文件长度换算单位
                function getFileSize($size){
                  $dw="Byte";

                  if($size >= pow(2, 40)){
                    $size=round($size/pow(2, 40), 2);
                    $dw="TB";
                  }else if($size >= pow(2, 30)){
                    $size=round($size/pow(2, 30), 2);
                    $dw="GB";
                  }else if($size >= pow(2, 20)){
                    $size=round($size/pow(2, 20), 2);
                    $dw="MB";
                  }else if($size >= pow(2, 10)){
                    $size=round($size/pow(2, 10), 2);
                    $dw="KB";
                  }else {
                    $dw="Bytes";
                  }
                  return $size.$dw;

                }

                getFilePro("demo.txt");
                getFilePro("hello");      
                    
                    
                    
               如果在缓存的10秒内，就从缓存文件中获取数据
              
                $cache=10;                   //缓存时间
              	$cachefile="cache.txt";      //缓存的文件

              if(file_exists($cachefile) && (time()-$cache) < filemtime($cachefile)) {
                echo file_get_contents($cachefile); //如果在缓存的10秒内，就从缓存文件中获取数据	

              }else{
                file_put_contents($cachefile, date("Y-m-d H:i:s", time()));
              }
                    
             
             
             
       3. 和文件路径相关的函数
 			
              相对路径：相对于当前目录的上级和下级目录

            .  当前目录
            ./php/apache/index.php
             php/apahce/index.php
             login.php
            ./login.php

            上一级目录
            ../images/tpl/logo.gif


           路径分隔符号
            linux/Unix    "/"
            windows       "\"

            DIRECTORY_SEPARATOR  为不同平台，在Windows \ Linux /

            不管是什么操作系统PHP的目录分割符号都支技 / (Linux)

            在PHP和Apache配置文件中如果需要指定目录，也使用/作为目录符号

            绝对路径：
            / 根路径

            /images/index.php

            指的操作系统的根
            指的是存放网站的文档根目录

             分情况
            如果是在服务器中执行（通过PHP文件处理函数执行）路径 则 “根”指的就是操作系统的根
            如果程序是下载的客户端，再访问服务器中的文件时，只有通过Apache访问，“根”也就指的是文档根目录

            http://www.xsphp.com/logo.gif


          basename(url)  返回路径中的文件名部分
          
 		       例子：
            
              $url1="./aaa/bbb/index.php";
              $url2="../www/yyy/login.rar";
              $url3="c:/appserv/www/demo.html";
              $url4="http://localhost/yyy/www.gif";

              echo basename($url1)."<br>";   //index.php
              echo basename($url2)."<br>";  //login.rar
              echo basename($url3)."<br>";  //demo.html
              echo basename($url4)."<br>";  //www.gif

    
        	dirname(url)   返回路径中的目录部分
         
           例子：
           
              	$url1="./aaa/bbb/index.php";
                $url2="../www/yyy/login.rar";
                $url3="c:/appserv/www/demo.html";
                $url4="http://localhost/yyy/www.gif";

                echo dirname($url1);    //      ./aaa/bbb
                echo dirname(dirname($url2));  //     ../www
                echo dirname($url3);                 //    c:/appserv/www
                echo dirname($url4);   //    http://localhost/yyy   
           
              
          
          
          
 *		   	pathinfo(url)    返回文件路径的信息(返回的是一个数组)

             例子：
              	$url1="./aaa/bbb/index.php";
                $url2="../www/yyy/login.rar";
                $url3="c:/appserv/www/demo.class.html";
                $url4="http://localhost/yyy/www.gif";
                echo '<pre>';
                print_r($path=pathinfo($url3));
                echo '</pre>';
	   
                输出
                    Array
                  (
                      [dirname] => c:/appserv/www
                      [basename] => demo.class.html
                      [extension] => html
                      [filename] => demo.class
                  )
                  
              这样可以获取随便一个
            echo $path["extension"];
             


     4. 文件的操作相关的函数（
             
             			创建文件 touch("文件名")
             			删除文件 unlink("文件路径");
             			移动文件 为文件重新命名 rename("当前文件路径"， “目录为文件路径”)
             			复制文件 copy("当前"， “目标”);
             			
             			一定要有PHP执行这个文件权限， Apache, 一个用户
             
             
       和权限设计有关的函数(这几个函数在Linux为主)
                

                chgrp -- 改变文件所属的组
                chmod -- 改变文件模式
                chown -- 改变文件的所有者

                filegroup -- 取得文件的组
                fileowner -- 取得文件的所有者





