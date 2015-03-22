---
layout : post
title: csdn top 5K password dict
tags: 
- csdn password,
- csdn top10000 password,
- csdn top 5K password,
---

由于是菜鸟，所以就直接引用前辈已经发的文章了[连接地址](http://hi.baidu.com/graylc/item/f146d50f5f402964d55a11f5)  

- 首先提取csdn的密码部分  

文件的内容都是按照 ```account # password # 123@email.com```这样的格式  

    cut -f 3 -d " " csdnpasswd > words.txt 

提取csdnpasswd文件里每行的第三部分，以" "为分隔符，把结果放到words.txt 文件里  

- 统计words.txt里的密码出现次数并排序并写入temp.txt  

取出现次数最多的前10000的密码  

    cat words.txt | sort | uniq -c | sort -k1,1nr | head -10000 >temp.txt

[此命令连接](http://blog.sina.com.cn/s/blog_5dce657a01012ddi.html)  

    sort:  对单词进行排序
    uniq -c:  显示唯一的行，并在每行行首加上本行在文件中出现的次数
    sort -k1,1nr:  按照第一个字段，数值排序，且为逆序
    head -10000:  取前10000行数据(即top 1W 的password)

- 删除密码前出现的次数  

这pass.txt 就是最终的密码字典~ :wink:  

    cat temp.txt | awk '{print $2}' > pass.txt

能力有限，勿笑  

在给一个sh脚本吧，也就是基于上面代码的合体 :sweat_smile:  

###pw.sh  

{% highlight bash lineos%}
#!/bin/sh
cut -f 3 -d " " csdnpasswd > words.txt
cat words.txt | sort | uniq -c | sort -k1,1nr | head -10000 >temp.txt
cat temp.txt | awk '{print $2}' > pass.txt
rm -rf words.txt temp.txt
echo "success"
{% endhighlight %}
 
{% gist anonymous/2759eb4104d30be7c0d5 pw.sh %}

> csdnpasswd 为密码文件名，此脚本请放在csdnpasswd同目录，若pw.sh不能运行，请chmod +x pw.sh  
> 若要统计别的密码文件，请对照修改提取密码部分的代码  
> 此代码在 kali 1.09a上成功运行  

