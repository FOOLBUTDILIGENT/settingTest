# settingTest

首先在res/xml下面建立preferencefragment.xml（注意，没有XML文件夹就自己建），在其中填写代码:
```
<?xml version="1.0" encoding="utf-8"?>
<PreferenceScreen xmlns:android="http://schemas.android.com/apk/res/android">
    <PreferenceCategory android:title="In-line preferences">
        <CheckBoxPreference
            android:key="checkbox preferences"
            android:summary="This is a checkbox"
            android:title="Checkbox_preference"
            />
    </PreferenceCategory>
    <PreferenceCategory android:title="Dialog-based preferences">
           <EditTextPreference
               android:dialogTitle="Enter your favorite animal"
               android:title="EditTextPreference"
               android:key="editText_preference"
               android:summary="An example that uses an edit text dialog"
               ></EditTextPreference>
        <ListPreference
            android:entries="@array/options"
            android:entryValues="@array/options_values"
            android:dialogTitle="Choose one"
            android:summary="An example that use a list dialog"
            android:title="List preference"
            android:key="list_preference"
            />
    </PreferenceCategory>
    <PreferenceCategory android:title="launch preferences">
            <PreferenceScreen
                android:key="screen_preference"
                android:summary="Shows another screen of preference"
                android:title="Screen preference"
                >
                <CheckBoxPreference
                    android:key="next_screen_checkbox_preferences"
                    android:title="Toggle preference"/>
            </PreferenceScreen>
           <PreferenceScreen
               android:summary="Launches an Activity from an intent"
               android:title="Intent preference">
               <intent
                   android:action="android.intent.action.VIEW"
                   android:data="http://www.baidu.com"></intent>
           </PreferenceScreen>

    </PreferenceCategory>
    <PreferenceCategory android:title="Preference attributes">
        <CheckBoxPreference
            android:key="parent_checkbox_preference"
            android:summary="This is visually parent"
            android:title="Parent checkbox preference" />
        <!-- 子类的可见类型是由样式属性定义的 -->
        <CheckBoxPreference
            android:dependency="parent_checkbox_preference"
            android:key="child_checkbox_preference"
            android:summary="This is visually a child"
            android:title="Child checkbox preference" />

    </PreferenceCategory>
</PreferenceScreen>
```
值得注意的是，在Listpreference中，arrays要自己在values文件夹中创建一个arrays.xml文件如下:
```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string-array name="options">
                <item>Total Cost</item>
                <item>Number of Stops</item>
                <item>AirLine</item>
            </string-array>
        <string-array name="options_values">
            <item>0</item>
            <item>1</item>
            <item>2</item>
        </string-array>
</resources>
```
在MainActivity.java的文件夹下创建PreFragment。java
```

import android.os.Bundle;
import android.preference.PreferenceFragment;
import android.support.annotation.Nullable;

public class PreFragment extends PreferenceFragment {
    @Override
    public void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        //从xml文件中加载选项
        addPreferencesFromResource(R.xml.preferencefragment);
    }

}
```
MainActivity.java:
```

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        FragmentManager fragmentManager=getFragmentManager();
        FragmentTransaction transaction=fragmentManager.beginTransaction();
        PreFragment preFragment=new PreFragment();
        transaction.add(R.id.layout1,preFragment);
        transaction.commit();
    }
}
```
效果图:
![1](https://raw.githubusercontent.com/FOOLBUTDILIGENT/images/master/settingTest/1.png)
![2](https://raw.githubusercontent.com/FOOLBUTDILIGENT/images/master/settingTest/2.png)
![3](https://raw.githubusercontent.com/FOOLBUTDILIGENT/images/master/settingTest/3.png)
![4-1](https://raw.githubusercontent.com/FOOLBUTDILIGENT/images/master/settingTest/4-1.png)
![4-2](https://raw.githubusercontent.com/FOOLBUTDILIGENT/images/master/settingTest/4-2.png)
![5-1](https://raw.githubusercontent.com/FOOLBUTDILIGENT/images/master/settingTest/5-1.png)
![5-2](https://raw.githubusercontent.com/FOOLBUTDILIGENT/images/master/settingTest/5-2.png)
