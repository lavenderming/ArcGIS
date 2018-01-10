参见：[Develop your first map app with Java](https://developers.arcgis.com/android/latest/guide/develop-your-first-map-app.htm)

- [概述](#%E6%A6%82%E8%BF%B0)
- [前置要求](#%E5%89%8D%E7%BD%AE%E8%A6%81%E6%B1%82)
- [在 Android Studio 中创建新项目](#%E5%9C%A8-android-studio-%E4%B8%AD%E5%88%9B%E5%BB%BA%E6%96%B0%E9%A1%B9%E7%9B%AE)
- [添加 ArcGIS Runtime SDK for Android AAR 依赖](#%E6%B7%BB%E5%8A%A0-arcgis-runtime-sdk-for-android-aar-%E4%BE%9D%E8%B5%96)
- [在布局中添加一个 MapView](#%E5%9C%A8%E5%B8%83%E5%B1%80%E4%B8%AD%E6%B7%BB%E5%8A%A0%E4%B8%80%E4%B8%AA-mapview)
- [在 MapView 上设置 map](#%E5%9C%A8-mapview-%E4%B8%8A%E8%AE%BE%E7%BD%AE-map)
- [构建和运行 app](#%E6%9E%84%E5%BB%BA%E5%92%8C%E8%BF%90%E8%A1%8C-app)

# 概述
该教程指导你用 ArcGIS Runtime SDK for Android 创建基本的地图 app，能用指定的初始地图范围显示地图，IDE 是 Android Studio。该指南为 Android Studio 3.0.1 编写 —— 不同版本的 Android Studio 可能在用户界面标题或选项的命名上有略微的不同。

你会使用 Java 语言来开发 app。此外，你也可以查看 [使用 Kotlin 的相同教程](https://developers.arcgis.com/android/latest/guide/develop-your-first-map-app-with-kotlin.htm)

你可以在 [Display a Map sample](https://developers.arcgis.com/android/latest/sample-code/display-map.htm) 示例中查看完整代码。

# 前置要求
在你开始前，确保下面这些你已完成：
- 符合 [系统要求](https://developers.arcgis.com/android/latest/guide/system-requirements.htm)
- 从 Google 下载 [Android Studio](http://developer.android.com/sdk/index.html)，Android 的官方 IDE。
- 知晓在 Android 平台开发 app 的基础知识和技术。更多信息见 [Android Developers homepage](http://developer.android.com/)

# 在 Android Studio 中创建新项目

当你运行 Android Studio，首先会显示 **Welcome** 屏。在这，你可以创建 Android app 项目。

1. 点击 **Start a new Android Studio project**。如果你已经打开了一个项目，你可以依次点击 **File > New > New Project**。
2. 在 **Application name** 文本框中输入 `Display map`。按需更改 **Company domain** 和 **Project location**，然后点击 **Next**。
    ![](https://developers.arcgis.com/android/latest/guide/GUID-14A0A568-FA38-4D81-90AE-BD4999ECF9A1-web.png)
3. 在 **Target Android Devices** 对话框，让 **Phone and Tablet** 处于选中状态，然后在 Minimum SDK 下拉框中选则 **API 16: Android 4.1**，然后点击 **Next**。
4. 在 **Add an Activity to Mobile** 对话框，点击 ** Empty Activity**，然后点击 **Next**。
5. 将向导的剩余选项保持默认，然后点击 **Finish**。
    
    一个新的 Android app 项目打开，显示一个默认布局

你现在已成功创建了一个包含一个 app 模块的 Android 项目。下一步你将添加 ArcGIS Runtime SDK for Android 依赖。

# 添加 ArcGIS Runtime SDK for Android AAR 依赖

接下来你要更新 gradle 构建脚本来向你的 app 模块中添加 ArcGIS Runtime SDK for Android 依赖。当你构建你的 app 时，它会自动从 Esri 公共 Bintray Maven repository 下载 Android Archive（AAR）包。

Android 是一个权限分离的系统。你还要为你 app 需要的功能添加权限。

1. 在 **Android project view** 小窗口的 **Gradle Scripts** 下，双击 **build.gradle (Project: \<project name\>)**。
    
    这打开了顶级的构建文件，该构建文件会作用到你项目的所有模块。如果你不熟悉 Gradle 构建系统，见 [Build System Overview](http://developer.android.com/sdk/installing/studio-build.html)。

1. 在脚本的 `allprojects/repositories` 块，如下所示添加一个新的 `maven` 块，值为 `url 'https://esri.bintray.com/arcgis'` 整个块看起来如下面代码所示：
    ```gradle
    allprojects {
        repositories {
            google()
            jcenter()
            
            // 添加 Esri 公共 Bintray Maven repository
            maven {
                url 'https://esri.bintray.com/arcgis'
            }
        }
    }
    ```

    该指令通过指定 Maven repository URL 告诉 Gradle 哪里去查找 ArcGIS Runtime SDK for Android 依赖。

1. 在 **Android project view** 窗口的 **Gradle Scripts** 下，双击 **build.gradle (Module: \<module name\>)**。

    这打开模块级的构建文件，该构建文件只会应用到项目中的单个 app  模块。如果你不熟悉 Gradle 构建系统，见 [Build System Overview](http://developer.android.com/sdk/installing/studio-build.html)。

1. 在脚本的 `dependencies` 块，添加一新行 `implementation 'com.esri.arcgisruntime:arcgis-android:100.2.0'`。该依赖块应该如下所示 —— 准确的依赖列表取决于 Android Studio 的版本和项目设置的选择。

    ```gradle
    dependencies { 
        implementation 'com.esri.arcgisruntime:arcgis-android:100.2.0' 
        implementation fileTree(dir: 'libs', include: ['*.jar'])
        [more dependencies...]
    }
    ```

    （在 Android 3.0 前，你应该使用 `compile` 代替 `implementation`）

1. 点击 Android Studio 工具栏上的 **Sync Project with Gradle Files**。此外，当你看到 gradle 脚本窗口顶部的 **Gradle files have changed since last project sync** 信息时，点击 **Sync Now**。

    ![](https://developers.arcgis.com/android/latest/guide/GUID-3FC8BBE7-FF01-4227-8BC4-0FE124C25A75-web.png)

1. 在 **Android project view** 窗口的 **app > manifests** 下，双击 **AndroidManifest.xml**。这打开了 app 的 manifest 文件

1. 添加如下 XML 元素作为现有 `manifest` 元素的子元素：
    ```gradle
    <uses-permission android:name="android.permission.INTERNET" /> 
    <uses-feature android:glEsVersion="0x00020000" android:required="true" />
    ```

    上述添加告知 Android launcher 你的 app 需要访问网络的权限。如果 app 运行于 API level 23 或以上，普通权限在安装时申请 —— 访问网络时普通权限，所以无需额外的工作来启用该权限。它还指明了你的 app 需要 OpenGL 2.0 版本的软件功能来支持其运行和显示 map view。你用 ArcGIS Runtime SDK for Android 开发的绝大多数 app 需要该功能和该最低权限。更多信息，见 Android 开发者指南中的 [Android Permissions](http://developer.android.com/guide/topics/security/permissions.html) 和 [Uses Feature Element](http://developer.android.com/guide/topics/manifest/uses-feature-element.html) 话题。

至此，你已经向你的 app 模块中添加了 ArcGIS Runtime SDK for Android AAR 依赖。下一步，你要给 app 添加一个地图来展示地图服务，并未该地图设置出事范围。

# 在布局中添加一个 MapView

至此，你已经向你的 app 模块中添加了 ArcGIS Runtime SDK for Android AAR 依赖。下一步是往 activity 布局中添加 `MapView`。

1. 在 **Android project view** 窗口，**app** 下，点击 **res > layout**，然后双击 **activity_main.xml**。这打开了 main activity 布局核心内容的 **Preview** 面板。注意取决于你使用的 Android Studio 版本和你选择的初始 activity 模板，项目可能会包含多份 XML 布局文件 —— 比如如果你选择了 **Basic Activity** 模板，你可能需要打开 **content_main.xml** 布局文件
2. 在窗口的左下方，点击 **Text** 显示布局的 XML 面板。默认情况下，这个 XML 布局文件中有两个标签。
    - 第一个标签是 `ConstraintLayout`。这是一个可以显示它内部其它 view 的 view。它按子 view 间的相对位置排列子 view。更多信息见 [Constraint Layout](https://developer.android.com/reference/android/support/constraint/ConstraintLayout.html) 和 [User Interface](http://developer.android.com/guide/topics/ui/index.html) 文档。
    - 第二个标签是 `TextView`，constraint 布局的子标签，显示 “Hello world!” 文本。
1. 选中整个 `TextView` 元素后将其替换为如下的 `MapView` 元素：
    ```xml
    <com.esri.arcgisruntime.mapping.view.MapView
        android:id="@+id/mapView"
        android:layout_width="match_parent"
        android:layout_height="match_parent" >
    </com.esri.arcgisruntime.mapping.view.MapView>
    ```

要更全面地了解用户界面（UI）设计的声明性方法，见：[Declaring Layout](http://developer.android.com/guide/topics/ui/declaring-layout.html)。此外，经常同 `ConstraintLayout` 一起使用的不同类型的布局约束属性，可以参见 [Constraint Layout](https://developer.android.com/reference/android/support/constraint/ConstraintLayout.html)

# 在 MapView 上设置 map
默认情况下，`MapView` 没有显示任何东西，所以下一步是定义要显示的 map。你将指定 map 显示来自 ArcGIS Online 的全球地形底图。对 app 而言，相比显示整个范围，初始时显示一特定区域比更有用，所以你需要设置 map 放大至一特定的点 —— 这里我们显示位于加利福利亚雷德兰兹的 Esri 校区。

1. 在 **Android project view** 窗口，**app** 下，点击 **java > [package name]**，然后双击 **MainActivity**。这会打开定义你 app 默认 activity 的 Java 代码。

2. 将下面类变量声明写到 `MainActivity` 类的顶部：
    ```java
    private MapView mMapView;
    ```

3. Android Studio 会在 `MapView` 类处用红色高亮，表明该类需要导入。把鼠标移到高亮处并按 Alt+Enter 来解析符号。选择导入：
    ```java
    import com.esri.arcgisruntime.mapping.view.MapView;
    ```

4. 添加如下代码到 `onCreate` 方法现有的 `setContentView` 调用之后：
    ```java
    mMapView = findViewById(R.id.mapView);
    ArcGISMap map = new ArcGISMap(Basemap.Type.TOPOGRAPHIC, 34.056295, -117.195800, 16); 
    mMapView.setMap(map);
    ```

    > 笔记：你需要导入
    > `com.esri.arcgisruntime.mapping.ArcGISMap` 和 `com.esri.arcgisruntime.mapping.Basemap`。

    上面的代码获取你定义在布局的 `MapView` 的引用（在 Android Studio 3.0 前，由 findViewById 返回的对象必须 cast 成 `MapView` 类型）。一个 `ArcGISMap` 对象由特定的预定义 `Basemap.Type`、特定中心位置坐标集、以及放大至指定级别定于后创建。然后，将 `ArcGISMap` 设置进 `MapView`

5. 添加下面的方法到 `MainActivity` 类，override 继承自父 activity 类的 `onPause` 和 `onResume` 方法，当这些方法被调用时暂停、重新运行 `MapView`：

    ```java
    @Override 
    protected void onPause(){
        mMapView.pause();
        super.onPause();
    }

    @Override 
    protected void onResume(){
        super.onResume();
        mMapView.resume();
    }
    ```

你现在已经完成将一个 ArcGIS Runtime SDK for Android map 添加到你的新 app 的所有步骤。现在可以开始构建和测试你的 app 了。

# 构建和运行 app

为测试你的 app，你需要连接到准备 debug 的设备上或创建并启动模拟器。更多信息见 [Using the emulator](http://developer.android.com/tools/devices/emulator.html) 或 [Using hardware devices](http://developer.android.com/tools/device.html)。

1. 在 Android Studio 工具栏上点击 **Run**
2. 在 ** Connected Devices** 对话框中选择你要用的设备或模拟器，然后点击 OK。
3. 当 app 在你的设备上打开后，它会显示加利福利亚雷德兰兹的街道地图。你可以双击地图来放大。

当你创建一个新项目，Android Studio 自动创建一个运行配置来在你的设备上启动 app。你会看到和下面所示截屏类似的界面。

> 小技巧：如果 app 运行但地图是空的，那么你需要检查 Android manifest 中是否正确添加了 `android.permission.INTERNET` 权限。

![](https://developers.arcgis.com/android/latest/guide/GUID-D87C0528-77F2-421B-858F-A77039266D39-web.png)

你已经完成了你的第一个  ArcGIS Runtime SDK for Android app。

别忘了你还可以在我们 GitHub 的 [Display a Map sample](https://developers.arcgis.com/android/latest/sample-code/display-map.htm) 上查看完整代码。