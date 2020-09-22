<div align="center">

## Check e\-mail address validity\(SMTP\)


</div>

### Description

In my work I am asking my self is there way to

check e-mail address validity.Here is one oh the decisions...
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Bogomil Shopov](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/bogomil-shopov.md)
**Level**          |Intermediate
**User Rating**    |4.6 (23 globes from 5 users)
**Compatibility**  |PHP 4\.0
**Category**       |[Internet/ Browsers/ HTML](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/internet-browsers-html__8-9.md)
**World**          |[PHP](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/php.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/bogomil-shopov-check-e-mail-address-validity-smtp__8-612/archive/master.zip)





### Source Code

<font size="2" face="Verdana"><b>Check e-mail address validity </b></font>
<p><font size="2" face="Verdana">In my work I am asking my self is there way to
 check e-mail address validity.Let's look over the following lines:<br>
 This is simple communication between user and SMTP server:</font></p>
<p><font size="2" face="Verdana"><i>(Server) 220 server5.donhost.co.uk ESMTP<br>
 (User) helo localhost<br>
 (Server) 250 server5.donhost.co.uk<br>
 (User) mail from:admin&lt;admin@purplerain.org&gt;<br>
 (Server) 250 ok<br>
 (User) rcpt to:contest&lt;contest@purplerain.org&gt;<br>
 (Server) 250 ok<br>
 (User) data<br>
 (Server) 354 go ahead<br>
 (User) subject:this is a test<br>
 (User) hello friend how are you?<br>
 .<br>
 (Server) 250 ok 1019555935 qp 93990 <br>
 (User) quit<br>
 (Server) 221 server5.donhost.co.uk </i></font></p>
<p><font size="2" face="Verdana">Then let's look over the following lines:</font></p>
<p><font size="2" face="Verdana"><i>(Server) 220 astral.acvilon.com ESMTP Sendmail
 8.11.6/8.11.6; Tue, 23 Apr 2002 13:43:10 +<br>
 0300<br>
 helo localhost<br>
 (Server) 250 astral.acvilon.com Hello [195.24.48.45], pleased to meet you<br>
 (User) mail from:htr@acvilon.com<br>
 (Server) 250 2.1.0 htr@acvilon.com... Sender ok<br>
 (User) rcpt to:bla_bla@acvilon.com<br>
 (Server) 550 5.1.1 bla_bla@acvilon.com... User unknown</i></font></p>
<p><font size="2" face="Verdana"><br>
 If web server support the user recognition, the result should be 'User unknown'</font></p>
<p><font size="2" face="Verdana"><b>PHP implementation</b></font></p>
<p><font size="2" face="Verdana" color="#0000A0">&lt;?PHP<br>
 class CEmail{</font></p>
<p><font size="2" face="Verdana" color="#0000A0">function check($host,$user){</font></p>
<p><font size="2" face="Verdana" color="#0000A0">$fp = fsockopen ($host, 25);<br>
 set_socket_blocking ($fp, true);<br>
 fputs ($fp, &quot;Helo Local\n&quot;);<br>
 fgets ($fp, 2000);<br>
 fgets ($fp, 2000);<br>
 fputs ($fp, &quot;Mail From:&lt;$user@$host&gt; \n&quot;);<br>
 fgets ($fp, 2000);<br>
 fputs ($fp, &quot;RCPT to:aetos&lt;$user@$host&gt; \n&quot;);<br>
 $result= fgets ($fp, 2000);<br>
 $st= substr($result,0,3);<br>
 if ($st==250){</font></p>
<p><font size="2" face="Verdana" color="#0000A0"> echo&quot;Email address is valid&quot;;<br>
 }<br>
 <br>
 else<br>
 echo&quot;The address is not valid&quot;;<br>
 <br>
 }<br>
 }</font></p>
<p><font size="2" face="Verdana" color="#0000A0">$m=new CEmail;<br>
 $m-&gt;check(&quot;acvilon.com&quot;,&quot;farkon&quot;);</font></p>
<p><font size="2" face="Verdana" color="#0000A0"> ?&gt;</font><font size="2" face="Verdana"><br>
 This class implementing the conversation in previous chapter (SMTP &amp; USER)</font></p>
<p><font size="2" face="Verdana"><br>
 <br>
 </font> </p>

