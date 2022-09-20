# PHP
## 判斷中文 two byte word
```
if (mb_strlen($string, mb_detect_encoding($string)) == strlen($string))
```

## Time calculate
```
$base = strtotime('11:30:29');
echo date('H:i:s', strtotime('+30 min', $base));
```

## Time functions
```
<?php
$today = '2013-04-19';
//年
echo date("Y-m-d", strtotime($today."+3 year"));
//月
echo date("Y-m-d", strtotime($today."-1 month"));
//週
echo date("Y-m-d", strtotime($today."+10 week"));
//日
echo date("Y-m-d", strtotime($today."+10 day"));
//時
echo date("Y-m-d", strtotime($today."+2 hour"));
//分
echo date("Y-m-d", strtotime($today."+20 minute"));
//秒
echo date("Y-m-d", strtotime($today."+5 seconds"));
?>

//加1天5秒
echo date("Y-m-d", strtotime($today."+1 day 5 seconds"));
//加1週減2天
echo date("Y-m-d", strtotime($today."+1 week -2 day"));
```

### diff time
```
date_default_timezone_set('Asia/Tokyo'); // you are required to set a timezone
$date1 = new DateTime('2009-08-12');
$date2 = new DateTime('2003-04-14');
$diff = $date1->diff($date2);
echo (($diff->format('%y') * 12) + $diff->format('%m')) . " full months difference";
```
