---
layout: post
title: "Final Exam Of The Sysu SE Android Class"
date: 2014-04-09 12:52:03 +0800
comments: true
categories: Android
keywords: android, java, exam, sysu

---

####在Android平台上实现一个本地应用——大学城特惠网

#####Some key codes
- 应用功能描述:
	- 1. 具有登录界面,可以输入账号和密码,并且有两个按钮“登录”和“退出”。如果点击“退出”按钮可以直接退出程序(如图一所示);
	- 2. 登录账号和密码可任意输入,当账号和密码非空且一样时视作合法。如果输入信息不合法时,显示“账号或密码错误!”(如图二,图三所示);
	- 3. 成功登录后显示主界面(如图四所示):主界面顶部显示登录界面输入的账号,下面是一个列表,显示特惠信息表中所有条目(每个条目显示学校与打折信息);
	- 4. 点击每个列表项可进入查看相应的特惠信息的明细(参照特惠信息表),点击“返回”按钮可以返回到主界面
	- 5. 附加功能:
		- 1, 使用对话框的形式代替原来输入非法登录信息的提示方式,要求如下:
			- i. 对话框给出提示文字;
			- ii. 包含两个按钮:点击“是”按钮后回到登录界面,点击“否”按钮后退出程序。
		- 2, 在桌面上显示本应用的 Widget 组件,要求如下:
			- i. 能显示一些关于本应用的信息(例如应用名);
			- ii. 包含一个按钮,点击此按钮后能启动本应用。
		- 3, 记住账号与密码,要求如下:
			- i. 程序退出后记住当前登录用户的账号与密码,重新打开本应用后能自动填充两个文本框。
		- 4, 记录用户登录的时间,要求如下:
			- i. 在主界面显示当前用户登录的时间(X 分 X 秒),并且能够实时刷新.
<!--more-->
```
public class MainActivity extends Activity {

	private Button login;
	private Button quitButton;
	private EditText nameEditText;
	private EditText pwdEditText; 
	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_main);
		login = (Button)findViewById(R.id.button2);
		quitButton = (Button)findViewById(R.id.button1);
		nameEditText = (EditText)findViewById(R.id.name);
		pwdEditText = (EditText)findViewById(R.id.pwd);
		
		login.setOnClickListener(new OnClickListener() {
			
			@Override
			public void onClick(View arg0) {
				// TODO Auto-generated method stub
				if(!nameEditText.getText().toString().equals("") && !pwdEditText.getText().toString().equals("") || (pwdEditText.getText().toString() == nameEditText.getText().toString())){
					Toast.makeText(MainActivity.this ,"login successfully", Toast.LENGTH_LONG).show();
					Intent intent = new Intent();
					intent.setClass(MainActivity.this, listplace.class);
					startActivity(intent);
					finish();
				}else{
					Toast.makeText(MainActivity.this ,"login failed", Toast.LENGTH_LONG).show();
				}
			}
		});
		
		quitButton.setOnClickListener(new OnClickListener() {
			
			@Override
			public void onClick(View arg0) {
				// TODO Auto-generated method stub
				finish();
			}
		});
		
		
	}

	@Override
	public boolean onCreateOptionsMenu(Menu menu) {
		// Inflate the menu; this adds items to the action bar if it is present.
		getMenuInflater().inflate(R.menu.main, menu);
		return true;
	}

}

```

```
package com.example.final_test1;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;

import android.app.Activity;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.AdapterView;
import android.widget.AdapterView.OnItemClickListener;
import android.widget.ListView;
import android.widget.SimpleAdapter;

public class listplace extends Activity{
	private ListView listView;
	private List<HashMap<String, String>> mdaList = new ArrayList<HashMap<String,String>>();
	
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.listplace);
		setData();
		listView = (ListView)findViewById(R.id.listView1);
		String from[] = new String[] { "info", "content" };
		int to[] = new int[] { R.id.info, R.id.content };
		SimpleAdapter spAdapter = new SimpleAdapter(this, mdaList, R.layout.listviewitem, from, to);
		OnItemClickListener clItemClickListener = new OnItemClickListener() {

			@Override
			public void onItemClick(AdapterView<?> arg0, View arg1, int arg2,
					long arg3) {
				Bundle bundle = new Bundle();
				bundle.putString("info", (String)mdaList.get(arg2).get("info"));
				bundle.putString("content", (String)mdaList.get(arg2).get("content"));
				bundle.putString("address", (String)mdaList.get(arg2).get("address"));
				bundle.putString("phone", (String)mdaList.get(arg2).get("phone"));
				
				Intent intent = new Intent();
				intent.setClass(listplace.this, c1.class);
				intent.putExtras(bundle);
				startActivity(intent);
				finish();
		
			}
		};
		listView.setAdapter(spAdapter);
		listView.setOnItemClickListener(clItemClickListener);
	}
	
	private void setData(){
		HashMap<String, String> map = new HashMap<String, String>();
		map.put("info", "中山大学特惠信息");
		map.put("content", "湖畔餐厅打折套餐");
		map.put("address", "内环东路中大生活区");
		map.put("phone", "135XXXX8888");
		mdaList.add(map);
		
		map = new HashMap<String, String>();
		map.put("info", "广东外语外贸大学特惠信息");
		map.put("content", "云山水榭，5折k歌");
		map.put("address", "内环东路广外生活区");
		map.put("phone", "136XXXX9900");
		mdaList.add(map);
		
		map = new HashMap<String, String>();
		map.put("info", "华南师范大学特惠信息");
		map.put("content", "华师体育用品");
		map.put("address", "中环西路华师生活区");
		map.put("phone", "137XXXX4458");
		mdaList.add(map);
	}

}

```

```
package com.example.final_test1;

import android.app.Activity;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;
import android.widget.TextView;

public class c1 extends Activity{
	private TextView tv ;
	private Button bt;
	
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.c1);
		tv = (TextView)findViewById(R.id.tv);
		bt = (Button)findViewById(R.id.b1);
		
		Bundle bundle = this.getIntent().getExtras();
		String infoString = bundle.getString("info");
		String addressString = bundle.getString("address");
		String contentString = bundle.getString("content");
		String phoneString = bundle.getString("phone");
		
		tv.setText(infoString + "\n" + addressString + "\n" + contentString + "\n" + phoneString + "\n");
		
		bt.setOnClickListener(new OnClickListener() {
			
			@Override
			public void onClick(View arg0) {
				// TODO Auto-generated method stub
				Intent intent = new Intent();
				intent.setClass(c1.this, listplace.class);
				startActivity(intent);
				finish();
			}
		});
	}
}

```

```
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    android:orientation="vertical"
    tools:context=".MainActivity" >

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginLeft="40dp"
        android:text="大学城特惠网"
        android:textSize="30dp" />

    <EditText
        android:id="@+id/name"
        android:hint="请输入您的账号"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:ems="10" >

        <requestFocus />
    </EditText>

    <EditText
        android:id="@+id/pwd"
        android:hint="输入登录密码"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:ems="10" />

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content" >

        <Button
            android:id="@+id/button2"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginLeft="150dp"
            android:text="登陆" />

        <Button
            android:id="@+id/button1"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="退出" />

    </LinearLayout>

</LinearLayout>

```

```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical" >

    <TextView
        android:id="@+id/textView1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="20dp"
        android:text="android会员你好" />

    <ListView
        android:id="@+id/listView1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" >
    </ListView>

</LinearLayout>

```

```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical" >

    <TextView
        android:id="@+id/info"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="TextView" />

    <TextView
        android:id="@+id/content"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="TextView" />

</LinearLayout>

```

```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    android:orientation="vertical" >

    <TextView
        android:id="@+id/tv"
        android:layout_width="fill_parent"
        android:layout_height="90dp"
         />

    <Button
        android:id="@+id/b1"
        android:layout_width="100dp"
        android:layout_height="wrap_content"
        android:text="返回" />

</LinearLayout>

```

