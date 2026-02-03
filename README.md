# data-analysis-for-weibo-scrapy
分享一个针对微博真假粉丝与用户画像的改良数据分析项目
啦啦哩哩 ʕง•ᴥ•ʔง，这里书接上回分享我改良后的代码，使用微博爬取出的数据.
主要修正点为：

1、修正使用 pyecharts 绘图的显示问题，解决方法为：下载pyecharts-assets到本地并将图片以网页版形式显示。

2、更改假粉丝判断方式

```# 昵称里包含“用户”的，基本上可以断定是假粉丝
data_fake = data[(data['user_follow_count']>5)&
                        (data['user_followers_count']>5)&
                        (data['user_screen_name'].str.contains('用户'))]
data_fake.shape```

```data['follow_ratio'] = data['user_follow_count'] / (data['user_followers_count'] + 1)
data_fake2=data[data['follow_ratio']>100]
data_fake2.shape```

```duplicate_image_count=data['user_profile_image_url'].value_counts()
suspicious_url=duplicate_image_count[duplicate_image_count>5].index
mask=data['user_profile_image_url'].isin(suspicious_url)
fake_image_data3=data[mask]
fake_image_data3.shape
```

3、针对真粉丝user_discription词云代码的修改更新<img width="1210" height="677" alt="b16a3695-8d38-426b-a798-96f0ecfc00d3" src="https://github.com/user-attachments/assets/803b299e-8e7d-4c75-9ac1-e718ab919a00" />



