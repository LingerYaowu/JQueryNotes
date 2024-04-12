## 10-JQuery Ajax

### $.ajax() 介绍
> 格式：$.ajax({ });
>    参数：
>        *1. type：请求方式GET/POST
>           2. url：请求地址url
>           3. async：是否异步，默认true异步
>           4. data：发送到服务器的数据
>           5. dataType：预期服务器返回的数据类型
>           6. contentType：设置请求头
>           7. success：请求成功时调用此函数
>           8. error：请求失败时调用此函数*
### $.ajax() 代码展示
#### index.html
```html
<input type="text" class="username">
<input type="password" class="passwd">
<button class="submit01">get请求</button>
<button class="submit02">post请求</button>
<script>
    var submitBtn01 = $('.submit01');
    var submitBtn02 = $('.submit02');

    // ajax get请求
    submitBtn01.click(function () {
        var un = $('.username').val();
        var pw = $('.passwd').val();
        if (un && pw) {
            $.ajax({
                type: 'get',
                url: 'get.php?username=' + un + '&passwd=' + pw,
                success: function (data) {
                    alert(data);
                }
            });
        } else alert('请将信息填写完整！');
    });

    // ajax get请求
    submitBtn02.click(function () {
        var un = $('.username').val();
        var pw = $('.passwd').val();
        if (un && pw) {
            $.ajax({
                type: 'post',
                url: 'post.php',
                // data使post请求独有的字段，用来存放post的数据，格式为json
                data: {
                    'username': un,
                    'passwd': pw
                },
                success: function (data) {
                    alert(data);
                }
            });
        } else alert('请将信息填写完整！');
    });
</script>
```
#### get.php
```php
<?php
$name = 'jiale';
$passwd = '0215song';
$usName = $_GET['username'];
$usPasswd = $_GET['passwd'];
if($usName == $name) {
    if($usPasswd == $passwd) {
        echo '登录成功！';
    } else echo '密码不正确！';
} else {echo '用户名不正确！';}
?>
```
#### post.php
```php
<?php
$name = 'jiale';
$passwd = '0215song';
$usName = $_POST['username'];
$usPasswd = $_POST['passwd'];
if($usName == $name) {
    if($usPasswd == $passwd) {
        echo '登录成功！';
    } else echo '密码不正确！';
} else {echo '用户名不正确！';}
?>
```
### $.get() / \$.post() 介绍
> 1. \$.get()
>       这是一个简单的GET请求功能以取代复杂的$.ajax()
>       请求成功时可调用回调函数，如果需要出错时执行函数，请用\$.ajax()
>       格式：\$.get('url',data,function(data,statu,xhr){},dataType);
>                   *url：请求的地址
>                   data：请求的数据，以json对象形式
>                   function(data,status,xhr)：请求成功运行的函数
>                       data：包含来自请求的结果数据
>                       status：包含请求的状态( success, notmodified, error, timeout, parsererror )
>                       xhr：包含xmlHttpRequest对象
>                   dataType：规定预期的服务器相应的数据类型*   
> 2. \$.post()
>       这是一个简单的POST请求功能以取代复杂的$.ajax()
>       请求成功时可调用回调函数，如果需要出错时执行函数，请用\$.ajax()
>       格式：\$.post('url',data,function(data,statu,xhr){},dataType);
>                   *url：请求的地址
>                   data：请求的数据，以json对象形式
>                   function(data,status,xhr)：请求成功运行的函数
>                       data：包含来自请求的结果数据
>                       status：包含请求的状态( success, notmodified, error, timeout, parsererror )
>                       xhr：包含xmlHttpRequest对象
>                   dataType：规定预期的服务器相应的数据类型*
### $.get() / \$.post() 代码展示
#### index.html
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>$.get()与$.post()</title>
    <script src="./script/jquery.min.js"></script>
</head>

<body>
    <input type="text" id="un">
    <input type="password" id="pw">
    <button class="getRes">get</button>
    <button class="postRes">post</button>
    <script>
        // get
        $('.getRes').click(function () {
            var un = $('#un').val();
            if (un) {
                $.get('$_get.php', { username: un, passwd: '0215song' }, function (data, status, xhr) {
                    alert(data);
                    console.log(status);
                    console.log(xhr);
                });
            } else alert('请将数据填写完整！');
        });
        // post
        $('.postRes').click(function () {
            var pw = $('#pw').val();
            if (pw) {
                $.post('$_post.php', { password: pw }, function (data, status, xhr) {
                    alert(data);
                    console.log(status);
                    console.log(xhr);
                })
            } else alert('请将数据填写完整！');
        });
    </script>
</body>

</html>
```
#### get.php
```php
<?php
$username = 'jiale';
$un = $_GET['username'];
if($username == $un) {
    echo '登录成功！';
} else echo '爬！';
?>
```
#### post.php
```php
<?php
$pw = '02150215';
$passwd = $_POST['password'];
if($pw == $passwd) {
    echo '密码正确！';
} else echo '密码错误！';
?>
```