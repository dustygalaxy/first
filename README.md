#登录界面   .php
<?php session_start();?>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>市政设计行业在线课程系统登陆界面</title>
    <link href="beginning.css" rel="stylesheet" type="text/css">
    <link href="main.css" rel="stylesheet" type="text/css">
</head>
<body style="font-family:Verdana, Geneva, sans-serif" onload="createCode()">
<script type="text/javascript" src="js.js"></script>
<div class="header">
    <ul class="headerleft" style="position:absolute; height: 64px">
        <li style="font-size:18px; color:#2d2e95; line-height:50px; list-style-type:none;">华北电力大学</li>
        <li style="font-size:12px; color:#000; line-height:10px; list-style-type:none;">www.ncepuvideo.com</li>
    </ul>
    <div class="most">慕课最好品牌</div>
    <ul class="headerright" style="position:absolute">
        <li><a href="...">慕课首页</a></li>
        <li><a href="...">上传视频</a></li>
        <li><a href="...">视频转码</a></li>
        <li><a href="...">观看视频</a></li>
        <li><a href="...">手机版</a></li>
        <li><a href="...">电脑版</a></li>
        <li><a href="...">帮助</a></li>
        <li><a href="...">常见问题</a></li>
    </ul>
</div>
<div class="main">
    <img src="picture/2c3acb00a7337b4f9ddc5f63d2bb937c.jpg" style="width: 630px;margin-top: 90px;margin-left: 20px;" />
    <img src="picture/23.png" style="margin-top: -298px;margin-left: -266px;"  />
    <div class="login">
        <ul class="loginhead" style="background-color:#FFF" id="nav1">
            <li style="width:0px; height:0px;"></li>
            <li class="currtwo"><a  href="..." id="two1" onmouseover="setContentTab('nav1','two',1)">用户登录</a></li>
            <li><a href="...."  id="two2" onmouseover="setContentTab('nav1','two',2)">管理员登陆</a></li>
        </ul>
        <div class="loginheadmain">
            <ul class="loginwrite" id="menu_con1">
                <div class="box12221" div id="con_two_1" style="display:block">
                    <form method="post">
                        <li>用户名:
                            <input type="text" placeholder="请输入用户名" style="width:160px; height:25px; margin-left:5px" name="user" />
                        <li>密码:
                            <input type="password" style="width:180px; height:25px; margin-left:5px"  name="psd"/>
                        </li>
                        <li>
                            <input type="checkbox" style="margin-left:10px" />
                            <a>十天免登陆</a><b>忘记密码？</b></li>
                        <div id="form1" runat="server" onsubmit="validateCode()">
                            <li>
                                <span style="font-size: 16px; position: absolute;top: 231px;">验证码：</span>
                                <div class="code" style="margin-left: 67px;font-size: 26px;border: 3px solid white; text-indent: 20px; width: 130px; height: 51px; line-height: 47px;" id="checkCode" onclick="createCode()" ></div>
                                <a style="float: right;margin-top: -56px;font-size: 12px;" href="#" onclick="createCode()">看不清换一张</a></li>
                            <li>
                                <span style="font-size:16px;">请输入验证码</span>
                                <input  style="float: right;margin-top: -37px;margin-right: 35px;" type="text"   id="inputCode" />
                            </li>
                            <li>
                                <input type="submit" name="submit" value="登陆" onclick="validateCode(); " style="width: 100px;height: 35px;margin-left: 25px;background-color: #4EA5D1;color: white;font-size: 18px; border-radius: 10px;" />
                                <input type="submit" value="去注册" style="width: 100px;height: 35px;margin-left: 40px;color: #4EA5D1;font-size: 18px; border-radius: 10px;" formaction="http://127.0.0.1/work/registerweb/register.php" />
                            </li>
                        </div>
                        <li style="color: #F00;font-size: 12px;margin-left: 10px;">提醒你谨防诈骗！！</li>
                    </form>
                </div>
                <div class="box12222" div id="con_two_2" style="display:none">
                    <form method="post">
                        <li>用户名:
                            <input type="text" placeholder="请输入用户名" style="width:160px; height:25px; margin-left:5px" name="manager" />
                        <li>密码:
                            <input type="password" style="width:180px; height:25px; margin-left:5px"  name="managerpsd"/>
                        </li>
                        <li>
                            <input type="submit" name="managersubmit" value="登陆" style="width: 100px;height: 35px;margin-left: 25px;background-color: #4EA5D1;color: white;font-size: 18px; border-radius: 10px;" />
                        </li>
                    </form>
                </div>
            </ul>
        </div>
    </div>
</div>
<div class="footer"> <img src="picture/timg.jpg" style="height:65px; margin-left:200px" />
    <ul class="footerword" style="position:absolute">
        <li><a href="...">慕课首页</a></li>
        <li><a href="...">视频观看问题</a></li>
        <li><a href="...">视频转码问题</a></li>
        <li><a href="...">视频上传问题</a></li>
        <li><a href="...">交流</a></li>
        <li><a href="...">意见建议</a></li>
    </ul>
</div>
</body>
</html>

//此处是与MYSQL进行交互验证用户名和密码
<?php
if(isset($_POST["submit"]) && $_POST["submit"] == "登陆") {
    $user = $_POST["user"];
    $psd = $_POST["psd"];
    $mipsd = md5($psd);
    //echo $mipsd;
    $_SESSION['username']=$user;
//造对象
    $db = new MySQLi("localhost", "root", "root", "db_work");
//判断是否出错
    !mysqli_connect_error() or die("连接失败！！");
//写sql语句
    $sql = "select password from member where username='{$user}'";
//执行SQL语句
    $result = $db->query($sql);
    $v = $result->fetch_row();
    if ($mipsd == $v[0]) {
       // header("Loccaltion:http://127.0.0.1/work/selfweb/self.php");//PHP跳转无法实现？
       echo "<script>window.location.href=\"http://127.0.0.1/work/selfweb/self.php\";</script>";
    } else {
        echo "<script>alert('您输入的用户名或密码不正确，请重新输入！！'); history.go(-1);</script>";
    }
}
?>
<?php
if(isset($_POST["managersubmit"]))
{
    $manager = $_POST["manager"];
    $_SESSION['managername']=$manager;
    echo $_SESSION['managername'];
    $managerpsd = $_POST["managerpsd"];
    $mimanagerpsd = md5($managerpsd);
    //造对象
    $db = new MySQLi("localhost", "root", "root", "db_work");
    //判断是否出错
    !mysqli_connect_error() or die("连接失败！！");
    //写sql语句
    $sql = "select password from manager where name='{$manager}'";
    //执行SQL语句
    $result = $db->query($sql);
    $v = $result->fetch_row();
    if ($mimanagerpsd == $v[0]) {
        // header("Loccaltion:http://127.0.0.1/work/selfweb/self.php");//PHP跳转无法实现？
        echo "<script>window.location.href=\"http://127.0.0.1/work/managerweb/manager.php\";</script>";
    } else {
        echo "<script>alert('您输入的用户名或密码不正确，请重新输入！！'); history.go(-1);</script>";
    }
}
?>

