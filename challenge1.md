# challenge1

## 시작

페이지의 소스코드가 다음과 같았다.

```php
<?php
  include "../../config.php";
  if($_GET['view-source'] == 1){ view_source(); }
  if(!$_COOKIE['user_lv']){
    SetCookie("user_lv","1",time()+86400*30,"/challenge/web-01/");
    echo("<meta http-equiv=refresh content=0>");
  }
?>
<html>
<head>
<title>Challenge 1</title>
</head>
<body bgcolor=black>
<center>
<br><br><br><br><br>
<font color=white>
---------------------<br>
<?php
  if(!is_numeric($_COOKIE['user_lv'])) $_COOKIE['user_lv']=1;
  if($_COOKIE['user_lv']>=6) $_COOKIE['user_lv']=1;
  if($_COOKIE['user_lv']>5) solve(1);
  echo "<br>level : {$_COOKIE['user_lv']}";
?>
<br>
<a href=./?view-source=1>view-source</a>
</body>
</html>
```

## 생각 방향

코드를 보면 아래쪽에 solve(1)라는 문장을 통해서 COOKIE값을 통해 조건문에 들어가 solve로 향해야 한다. 

따라서 쿠키값을 조작을 해야하는 것을 인지했는데 문제점이 user_lv >= 6인 부분에서 다시 1로 설정이 되는 것이다. 따라서 저 조건문을 넘기고 다음 if문을 가는것이 문제였다. 

## 결론

데이터를 너무 단순하게 생각했다. 5 다음에 6이라는 정수형 타입에 고정이 되어있어서 잠깐 해맸지만 **5.5라는 6~5사이값을 user_lv값에 대입**해줌으로써 해결을 했다.

덕분에 크롬의 분석도구인 Application도구도 처음 써보고 쿠키에대한 정보를 확인 할 수 있다는 것을 깨달은 단계였다.