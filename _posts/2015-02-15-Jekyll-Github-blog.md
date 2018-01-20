---
title:  Jekyll + Github - Construction of the road for personal blog
---
Jekyll build personal blog,said in front, then we need to do a lot of things. Including environment configuration, account registration, domain name purchase (not required) and so on. Wants to engage in a before and after have their own blog, for 16 years I bought a domain name at a price of 16 yuan, "saying the domain name renewals little Guia .." with python and pitched an offline blog let the matter rest " critical deployments too much trouble ... " Until a few sprouted out of another to build a blog's mind, he was again huh. Fortunately, after several days of messing around, get out.
### Several key elements of
- Jekyll
   - Ruby
   - DevKit
   - Pygments
   - Python
- Github
   - account
   - client
- Domain
- Sites statistics
   - Baidu
   - Google
- Commenting system

> Step by step to build their own web blog

- Established github
    - registration github.
    - The establishment of a warehouse. Warehouse named <user name> .github.io, please refer to the detailed blog github create a personal blog 
   - above are operating on github page. In order to facilitate the testing and subsequent installation of the update blog github client.
- Domain name and other settings
  - Mine is from Ali cloud purchased website. You can also go to other places. Registered users, select the right domain name, payment (Alipay, more convenient). You then need to bind the domain name space, find the domain name server management business management.
  - Figure out seven cattle home. Free version of the currently good enough, put some pictures relatively easy
- To install Jekyll "can also be used linux"on
  - reference Windows:Jekyll install on Windows.After installation Jekyll. Open github client login. Before the establishment of the warehouse to the local clone. For example, I: dearLilian.github.io, clone to d: // lilian / down. We will see d: the emergence of // lilian / file under a folder named dearLilian.github.io.
- Review and site statistics
  - First,website statistics, you need to Baidu statistics Google Analytics Registered account, and extract the corresponding id (for details of operation baidu or google) such as my baidu id is e572ae9801b3a18891f123796b889f77, google id to UA-88738012-1, later use.
Second, it is the site of the comment management system,to say(I click to install) the registered account, set the domain name. For example, I was www.robotkang.duoshuo.com. That is to say the user name robotkang (will be used later) say has been linked to! Now used on this site is Valine comment system, details  https://valine.js.org/#/Reference:
- select a blog template
   - for example, I chose baixinha blog template. If you like, you can download this down.can go my github.I fork on
modifying the template for your blog
   - Aftertemplate above will download, unpack. And leopard pan.github.io-master inside the file copy to kangblog.github.io folder. At this point, if you turn on Jekyll services, namely: command line mode input

>jekyll serve

- Open the browser: localhost: 4000, this time you can see the original author (baixin) of blog.
So now modify the template, showing you something. (For easy editing various formats of files, we recommend pre-installed sublime Text)
working
1. modify the configuration file
>> first open_config.ymlmodify file where you want to modify.
Need to modify the project
titile:include:Your blog title
subtitle:Your blog subheading
description:Your blog description
avatarTitle:your avatar in the title
avatarDesc:describe your avatar
url:domain name into your
commentin theduoshuo: change your user name to say
socialinside
weibo:your meager id (not the user nickname)
github:github username of your
mail:your mailbox
can complement the other, can not not write, the original text can be deleted
 id:baidu:your baidu statistics id:
 idga:your Google Analytics's id
2. modify the domain namethe configuration fileCNAME
modifyfor your own domain name, such  robotkang.ccas:if there is no direct emptied (behind access when, direct access to your github page can)
3. modify personal filesabout.md
here should be modified for your own presentation. (Required markdown will be basic grammar.)
4. picture
if you want to use your own avatar, then open theimagesfolder, your own avatar pictures in that folder and rename it toavatar.jpg.
5. the site icon
if you want to use your own personal website icons, the same picture on your icon in the folder and rename it tofavicon.png.
6. blog posts
  - last is your blog content.open the_postsfolder, you can delete the original files are lost, then edit your own blog.
There, you have to create a new blog content contained in the first six rows, wheretitletheto write your own blog title,dateafter thewritten on your own time (but the format should be consistent),tag.write your own label after the  Behind the content is the content markdown syntax. Save the above file,named:2016-08-04-MyFirstBlog.md.
   - At this point restart jekyll service

jekyll serve


and then openlocalhost:4000,open the blog home page, you can see this blog you just released the.
