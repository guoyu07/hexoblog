title: 【转载】RSA信任关系失效
date: 2014-08-13 01:53:15
tags: RSA
---

原文： http://blog.sina.com.cn/s/blog_6c9eaa150100rpot.html

when I ssh to log on the server,
there is a error msg: 


	@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
	@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
	@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
	IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
	Someone could be eavesdropping on you right now (man-in-the-middle attack)!
	It is also possible that the RSA host key has just been changed.
	The fingerprint for the RSA key sent by the remote host is
	28:5d:a3:42:1f:ac:d5:2b:9a:6a:b1:28:b1:6b:55:f8.
	Please contact your system administrator.
	Add correct host key in /home/whfwind/.ssh/known_hosts to get rid of this message.
	Offending key in /home/whfwind/.ssh/known_hosts:2
	RSA host key for 192.168.100.5 has changed and you have requested strict checking.
	Host key verification failed.

then I searched on the internet, so I collected here:
you just need to delete or annote the line of your home ~/.ssh/known_host file of the IP you have failed logged 


