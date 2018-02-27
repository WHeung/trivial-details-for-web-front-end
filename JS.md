
## 正则表达式匹配但不捕获

### String.match(RegExp)

```
/* 用括号()的方法可以  分开 匹配但不捕获内容 和 匹配并捕获的内容， 但用该方法时不能使用全局匹配
*/
'abc'.match(/a(b)c/)     // 得到 ['abc', 'b']
'abc'.match(/a(b)c/)[1]     // 得到 ['b']
'abc'.match( /a(b)c/g)     // 得到 ['abc']

/*要使用全局匹配的话需要先分组抽出内容 , 再每组使用 match 查找或者 replace 替换
*/
var html = '<p>内容1</p>\n<p>内容2</p>\n<p>内容3</p>'
html = html.match(/<[^>]+>[^<]*<\/[^>]+>/ig) // ["<p>内容1</p>", "<p>内容2</p>", "<p>内容3</p>"]
data = html.map(item => {
    // replace
    item = item.replace(/<\/?[^>]+>/ig, '')
    return item
    // match
    item = item.match(/<[^>]+>([^<]*)<\/[^>]+>/i)[1]
    return item
}) //得到 ["内容1", "内容2", "内容3"]
```

### RegExp.exec(String)

```
/* 在调用非全局的 RegExp 对象的 exec() 方法时，返回的数组与调用方法 String.match() 返回的数组是相同的
*/
/* 在调用全局的 RegExp 对象的 exec() 方法时，在循环中反复地调用 exec() 方法获得信息
*/
const html = '<p>内容1</p>\n<p>内容2</p>\n<p>内容3</p>'
const RegExp = /<[^>]+>([^<]*)<\/[^>]+>/ig
var data = []
let item
while((item = RegExp.exec(html)) !== null) {
    data.push(item[1])
} //得到 ["内容1", "内容2", "内容3"]
```

### 表单range双滑块区间组件
```
<!DOCTYPE html>
<html>
<head>
<meta  charset="utf-8" />
<title> js双滑块区间 </title>
<style type='text/css'>
#range{position:relative;width:148px;height:2px;font-size:0;line-height:0;background:#fff;border:1px inset #9C9B97}
#meaBox{position:absolute;width:148px;height:4px;background:#ccc;top:-2px;border:1px inset #9C9B97;border-left:0;border-right:0;}
.mea{position:absolute;top:-5px;width:2px;height:10px;border:3px solid #fff;border-top:13px solid #3f8e55;}
#mea_l{left:0;}
#mea_r{right:0;border-top:13px solid #ff0000;}
</style>
</head>
<body>
<div id='range'>
	 <div id='meaBox' onmousedown="change(this,event)"> </div>
     <div id='mea_l' class='mea' onmousedown="change(this,event)" ></div>
	 <div id='mea_r' class='mea' onmousedown="change(this,event)" ></div>
</div>

<script type='text/javascript'>
var $id=function(o){return document.getElementById(o) || o;}
var change=function(o,e){
	var e = e ? e : window.event;
	if(!window.event) {e.preventDefault();}
	var init={
		mX: o.offsetLeft,
		lX: $id('mea_l').offsetLeft,
		rX: $id('mea_r').offsetLeft,
		dX: e.clientX
	};
	document.onmousemove=function(e){
		var e = e ? e : window.event;
		var dist=e.clientX-init.dX,
			len=init.mX + dist,
			l_x=init.lX,
			r_x=init.rX;
		switch ($id(o).id){
			case 'mea_l':
				l_x=init.lX + dist;
				move();
				break;
			case 'mea_r':
				r_x=init.rX + dist;
				move();
				break;
			case 'meaBox':
				l_x=init.lX + dist;
				r_x=init.rX + dist;
				move2();
				break;
			default: break;
		}
		
		function move(){
			if(r_x > l_x + 20 && len>=0 && len<=140 ) {
				o.style.left=len+"px";
				$id('meaBox').style.left= l_x + 'px';
				$id('meaBox').style.width=r_x - l_x + 'px';
			}
		};
		function move2(){
			if(l_x>=0 && r_x <=140 ) {
				o.style.left=len+"px";
				$id('mea_l').style.left= l_x + "px";
				$id('mea_r').style.left= r_x +"px";
			}
		};
	}
	document.onmouseup=function(){
		document.onmousemove=null;
		document.onmouseup=null;
	}
}
</script>
</body>
</html>
```

## JSON.parse的坑

### JSON.parse数字或数字形字符串时会进行一定程度的四舍五入
```
JSON.parse('171226103549893567955') // 171226103549893570000
JSON.parse(171226103549893567955) // 171226103549893570000
```
