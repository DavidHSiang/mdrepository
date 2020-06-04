---
title: Okhttp3基本使用
date: 2020-04-11 13:58:36
reward: true
declare: true
tags: 
	- Android
categories: 
    - [移动开发,Android]
---

### 1.安装OkHttp3
在build.gradle中添加依赖

``implementation 'com.squareup.okhttp3:okhttp:3.10.0'``

[官网网址： https://github.com/square/okhttp](https://github.com/square/okhttp)

### 2.异步Get请求

异步GET请求的4个步骤：

1.创建OkHttpClient对象

2.通过Builder模式创建Request对象。

3.通过request的对象去构造得到一个Call对象。

4.通过call.enqueue方法，来提交异步请求。以异步的方式去执行请求，将call加入调度队列，任务执行完成会在Callback中得到结果。

<!--more-->

```java

 private void getRequest() {
 		//0.创建url对象，用于存放要访问的地址
 		String url = "http://wwww.baidu.com";
        //1.创建OkHttpClient对象
        OkHttpClient okHttpClient = new OkHttpClient();
        //2.创建Request对象，设置一个url地址,设置请求方式。
        Request request = new Request.Builder().url(url).method("GET",null).build();
        //3.创建一个call对象,参数就是Request请求对象
        Call call = okHttpClient.newCall(request);
        //4.请求加入调度，重写回调方法
        call.enqueue(new Callback() {
            //请求失败执行的方法
            @Override
            public void onFailure(Call call, IOException e) {
            }
            //请求成功执行的方法
            @Override
            public void onResponse(Call call, Response response) throws IOException {
                String data = response.body().string();
                Log.d("response",data);
                runOnUiThread(new Runnable() {
                    @Override
                    public void run() {
                        //更新UI
                    }
                });
            }
        });
    }
```

### 3.同步Get请求 （较少用）

* 前面几个步骤和异步方式一样，只是最后一部是通过 ``Call.execute() ``来提交请求

* 注意：这种方式会**阻塞**调用线程，所以在Android中应放在**子线程**中执行，否则有可能引起**ANR异常**，**Android3.0** 以后已经**不允许在主线程访问网络**。

```java
		//0.创建url对象，用于存放要访问的地址
 		String url = "http://wwww.baidu.com";
		//1.创建OkHttpClient对象
        OkHttpClient okHttpClient = new OkHttpClient();
        //2.创建Request对象，设置一个url地址（百度地址）,设置请求方式。
        Request request = new Request.Builder().url(url).method("GET",null).build();
        //3.创建一个call对象,参数就是Request请求对象
        Call call = okHttpClient.newCall(request);
        //4.同步调用会阻塞主线程,这边在子线程进行
        new Thread(new Runnable() {
                @Override
                public void run() {
                    try {
                        //同步调用,返回Response,会抛出IO异常
                        Response response = call.execute();
                    } catch (IOException e) {
                        e.printStackTrace();
                    }
                }
            }).start();
```

### 4.异步POST——键值对

```java
private void postAsynHttp() {
	 //1.创建OkHttpClient对象
     mOkHttpClient=new OkHttpClient();
     RequestBody formBody = new FormBody.Builder()
             .add("size", "10")
             .build();
     Request request = new Request.Builder()
             .url("http://api.1-blog.com/biz/bizserver/article/list.do")
             .post(formBody)
             .build();
     Call call = mOkHttpClient.newCall(request);
     call.enqueue(new Callback() {
         @Override
         public void onFailure(Call call, IOException e) {
         }
         @Override
         public void onResponse(Call call, Response response) throws IOException {
             String str = response.body().string();
             runOnUiThread(new Runnable() {
                 @Override
                 public void run() {
                     Toast.makeText(getApplicationContext(), "请求成功", Toast.LENGTH_SHORT).show();
                 }
             });
         }
     });
 }
```

-----

## 参考文档

[OKHttp3 基本用法](https://www.jianshu.com/p/16ab28d40737):https://www.jianshu.com/p/16ab28d40737

[Okhttp3基本使用](https://www.jianshu.com/p/da4a806e599b):https://www.jianshu.com/p/da4a806e599b
