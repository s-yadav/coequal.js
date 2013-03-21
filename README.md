coequal.js
==========

coequal is a small utility function to check all type data types and objects in javascript.
<p>coequal perform a deep comparison to find equality of data and objects. For different objects conditions are different. Let see all senarios.</p>
<strong>1. Array</strong> :  Array of any data types are supported for comparision.
For ex:
<pre><code>

var a=[1,2,3] ,b=[1,2,3]
coequal(a,b) //returns true;
 
var a=[{b:"b",d:"d"} ,{e:"e",f:"f"}] ,b=[{b:"b",d:"d"} ,{e:"e",f:"f"}];
coequal(a,b) //returns true;
</code></pre>
Javascript array also support array of different dataType in same array (But making array this way is not suggested.)
<pre><code>
var a=[1,{e:"e",f:"f"}] ,b=[1,{e:"e",f:"f"}];
coequal(a,b) //returns true
</code></pre>
If for you order of element does not matter for comparision
<pre><code>
var a=[1,2,3] ,b=[1,3,2]
coequal(a,b,{orderCheck:false}) //returns true
</code></pre>

<strong>2. Object</strong>: In object it checks the key, value pair must be same and equal upto the end level of json.
<pre><code>
var a={
"k1":"b",
"k2":{
        "k3":"abc"
    }
}
var b={
 "k2":{
        "k3":"abc"
},
"k1":"b"
}
coequal(a,b) //returns true
</code></pre>
<strong>3.Function </strong>:
There are two options for comparing function. Compare by code compare by constructor. Default is constructor.
<pre><code>
var a=function(){
alert("a");
}
var b=function(){
alert("a");
}
var c=a;
coequal(a,b) //return false;
coequal(a,b,{functionCheck:"code"}) //return true
coequal(a,c) //return true;
</code></pre>

<p><strong>4. Dom object</strong> :
  Document object can be of two type
</p>
<p> i. Collection  </p>
<p>ii. Element</p>
<p> If you want to compare collection to collection or collection to element you need to activate collectionCheck in option. ie : option will be : { collectionCheck :true}
  You can compare svg and canvas element also. </p>
<pre><code>
&lt;img src=&quot;images/image.png&quot; class=&quot;image&quot;  id=&quot;myimage&quot;/&gt;<br />
<p>&lt;svg xmlns=&quot;http://www.w3.org/2000/svg&quot; version=&quot;1.1&quot;&gt;<br />
  &lt;circle id=&quot;mycircle&quot; cx=&quot;100&quot; cy=&quot;50&quot; r=&quot;40&quot; stroke=&quot;black&quot; stroke-width=&quot;2&quot; fill=&quot;red&quot; /&gt;<br />
&lt;/svg&gt;<br />
    var img1=document.getElementsByClassName('image');
    var img2=document.getElementById(' myimage ');
    var img3=document.getElementsByTagName('img');
    var cir=document.getElementById("mycircle");
       var cir2=document.getElementById("mycircle");

    coequal(img1, img3) //return false;
    coequal(img1, img2) //return false;
    coequal(img1, img3,{collectionCheck:true}) //return true;
    coequal(img1, img2,{collectionCheck:true}) //return true;
    coequal(cir, cir2) //return true;
</p></code></pre>

<strong>4. Date object</strong> :
Date object are compared by milliseconds from those objects.
<pre><code>
var date1=new Date('05/03/2013');
var date2=new Date('05/03/2013');
coequal(date1, date2) //return true;
</code></pre>

<strong>5. Regex object</strong> :
Rexed object are converted to string and compared.
<pre><code>
var rg1=/[1-9]/g;
var rg2=/[1-9]/g;
var rg3=new RegExp('[1-9]','g');

coequal(rg1, rg2) //return true;
coequal(rg1, rg3) //return true;
</code></pre>

<strong>6. string or number</strong> :
For string or number dont use this method because they are directly comparable. But even though you can compare it.<br>
<pre><code>
coequal(2345,2345 ) //return true;
coequal('abcd', 'abcd') //return true;
</code></pre>

<p><strong>Options</strong></p>
<table width="100%%" border="0" cellspacing="0" cellpadding="0">
  <tr>
    <td>Option</td>
    <td>Allowed values</td>
    <td>Default</td>
    <td>Description</td>
  </tr>
  <tr>
    <td>functionCheck</td>
    <td>code,constructor (string)</td>
    <td>constructor</td>
    <td>If setted as code it only checks the code within the function. It does not check the protypes.<br />
      As constructor it check only by refrence.<br />
      Used if you want to compare function.</td>
  </tr>
  <tr>
    <td>orderCheck</td>
    <td>true,false (boolean)</td>
    <td>true</td>
    <td>If true , the array element must be on same order than only it is treated as equal.&nbsp;If false elements can be on any order.</td>
  </tr>
  <tr>
    <td>collectionCheck</td>
    <td>true,false(boolean)</td>
    <td>false</td>
    <td>If you want to compare collection to collection or collection to element you need to set it as true.</td>
  </tr>
</table>
<br />
<br />
<strong>Limitation</strong><br />
1. Object must not be cyclic object, else it ill go on ifinite loop.
