参见：[Install the SDK](https://developers.arcgis.com/android/latest/guide/install-and-set-up.htm)

- [概述](#%E6%A6%82%E8%BF%B0)
- [Gradle](#gradle)
    - [需要请求的权限与功能](#%E9%9C%80%E8%A6%81%E8%AF%B7%E6%B1%82%E7%9A%84%E6%9D%83%E9%99%90%E4%B8%8E%E5%8A%9F%E8%83%BD)

# 概述
这里开始为你的开发环境设置 ArcGIS Runtime SDK for Android。在同一台机器上你可以有不同版本的上述 SDK。你也可以在同一机器上同时拥有上述 SDK 和其它 ArcGIS Runtime SDK。

> 笔记：
> 开发 ArcGIS Runtime app 无需许可，你的开发机无需授权。作为 [ArcGIS 开发者计划](https://developers.arcgis.com/announcements/) 的成员，你拥有免费的 [ArcGIS 开发者订阅（基础计划）](https://developers.arcgis.com/pricing)。通过该计划，你可以下载并安装任意 ArcGIS Runtime SDK 并立即拥有访问 API 所有功能的权限。你可以免费 [成为上述开发者计划的一员](https://developers.arcgis.com/sign-up)。

# Gradle

我们建议通过 Gradle 安装，这样会安装必要的依赖并从 [Bintray Esri repository](https://bintray.com/esri/arcgis/arcgis-android) 安装 SDK 二进制文件。更多完整步骤的详细信息，见 [Develop your first map app](https://developers.arcgis.com/android/latest/guide/develop-your-first-map-app.htm) 更多关于 Gradle 的信息，见 [https://gradle.org](https://gradle.org/)。

1. 在项目的 `build.gradle` 文件，`repositories` 块内，添加一个把 Esri 的 maven repository URL 添加到你的项目的指令。Esri 的库不是开源的，因此该库不在该脚本的默认库中，所以你必须指定该 URL
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

1. 在 app 模块的 `build.gradle` 文件，在 `dependencies` 块，添加一条将 ArcGIS Runtime SDK for Android 依赖包含到你的 app 中的指令

    ```gradle
    dependencies { 
        implementation 'com.esri.arcgisruntime:arcgis-android:100.2.0' 
        [...]
    }
    ```

1. 取决于你要在 app 中添加什么 ArcGIS，你还需要在你的 manifest 文件中添加声明，如[接下来的部分所述](https://developers.arcgis.com/android/latest/guide/install-and-set-up.htm#ESRI_SECTION2_4D942FD949B74D29B890DA771CEDDD5B)。

1. 此外，取决于你要在 app 中使用什么运行时功能，下面的步骤你可能也需要执行

    - 如果你的 app 使用 StreetMap Premium data，如 [Add StreetMap Premium data](https://developers.arcgis.com/android/latest/guide/add-streetmap-premium-data.htm) 所述，下载你要的区域。
    - 如果你的 app 使用 [grid-based transformations](https://developers.arcgis.com/android/latest/guide/spatial-references.htm#ESRI_SECTION2_05EBF84543B1438D9FA51D50168230DF)，从 [developers.arcgis.com 的下载页](https://developers.arcgis.com/downloads) 下载支持的 Projection Engine 文件
    - 如果你的 app 要显示 [ENC 层](https://developers.arcgis.com/android/latest/guide/display-electronic-navigational-charts.htm)，从 [developers.arcgis.com 的下载页](https://developers.arcgis.com/downloads) 下载水文目录。

到此你已准备好用 ArcGIS Runtime SDK for Android 开发了！你可能想试试 [开发你的第一个地图 app](https://developers.arcgis.com/android/latest/guide/develop-your-first-map-app.htm)，或直接到 [示例](https://developers.arcgis.com/android/latest/sample-code/) 或 [API 参考](https://developers.arcgis.com/android/latest/api-reference/)。

## 需要请求的权限与功能

