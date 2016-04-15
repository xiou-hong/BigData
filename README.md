<h1>Collecting Twitter data</h1> 
抓取Twitter的資料


OS: Ubuntu
Tool:elasticsearch,logstash,JDK8

elasticsearch
https://www.elastic.co/downloads/elasticsearch

logstash
https://www.elastic.co/downloads/logstash

JDK 8
http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html

<h2>Step 1</h2>
首先先來寫 logstash 所需要的 conf 檔
(conf 的目的是用來執行資料的input以及output，而本程式是從Twitter上抓資料存到elasticsearch)
<br>
input{<br>
   	twitter {
	   <br> consumer_key => "keysZrLu8HMy7ClT7OpSVQ"
	   <br>consumer_secret => "KpUUKjKxN2PhimaWhWsF3BhFcbBfL35JuRnsqVWHxM"
	   <br>oauth_token => "1257251456-IAivxyVmYtC7w4pnQRbxfVnuCJrnDeOZox5v8Y3"
	   <br>oauth_token_secret => "kJXkOUAVt0zsqb3vnoGoxKFn5LVbncbeKmIodWFan87cv"
	   <br>keywords => ["a"]
	   <br>full_tweet => true
	<br>}</div>
<br>}
<br>output{
	<br>elasticsearch{
	   <br> index => "twitter"
<br>}
<br>}

之後執行此conf (利用$./logstash -f twitter.conf)
就會開始抓取資料

<h2>Step 2</h2>
抓好足夠的資料量
接者再寫一個conf
input 這次改成elasticsearch
output 改成 file
即可存成json


input{<br>
   	elasticsearch {
	  <br>index=>"剛剛你抓twitter conf的名稱"
	<br>}</div>
<br>}
<br>output{
	<br>file{
	   <br> path => "放路徑名稱及檔名"
<br>}
<br>}














