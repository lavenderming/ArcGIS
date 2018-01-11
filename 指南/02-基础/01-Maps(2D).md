参见：[Maps(2D)](https://developers.arcgis.com/android/latest/guide/maps.htm)

- [概述](#%E6%A6%82%E8%BF%B0)
- [在线 map](#%E5%9C%A8%E7%BA%BF-map)
- [离线 map](#%E7%A6%BB%E7%BA%BF-map)
    - [服务模式（Services patterns）](#%E6%9C%8D%E5%8A%A1%E6%A8%A1%E5%BC%8F%EF%BC%88services-patterns%EF%BC%89)
    - [桌面模式（Desktop pattern）](#%E6%A1%8C%E9%9D%A2%E6%A8%A1%E5%BC%8F%EF%BC%88desktop-pattern%EF%BC%89)

# 概述

地图可以讲述故事、体现想法或展示情况。 它可以帮助你完成数以百计的事，从查找最近的医院到观看与人口密集地区有关的地震事件。

不像大多数地图，ArcGIS 地图有许多额外的功能。它们可以包含由层组织的数据且拥有分析能力，能让你发现模式并解决许多类型的问题。例如，一个 ArcGIS 地图可以向你展示一卡车队在某区域内的移动路径，并且它可以优化这些的路径来最大化车队效率。

一个地图通常由提供地理环境的底图（basemap）和包含地图重要内容的操作层组成。你可以在你的 app 地图内使用你自己的数据，Esri 的数据，或两者混合使用。在 ArcGIS Runtime app 中，一个 map 可以和 map view 一起使用来在屏幕上显示地理数据。在这种情况下，map 作为 MVC 架构中的 model 层，map view 作为 view 层：

- map 指定了地理内容（数据）来自哪里且应该如何组织（它有哪些层，什么 bookmark，初始 viewpoint 等）。各层的内容可能来自各种各样的[地图源](https://developers.arcgis.com/android/latest/guide/maps.htm#ESRI_SECTION1_FC86B8F7930B4D6C91484EBC7F381CFB)，包括在线的数据源或本地存储的数据，例如移动地理数据库中的要素表或移动地图包中的数据。更多关于你可以包含进 map 的数据和层类型，见 [Layers and tables](https://developers.arcgis.com/android/latest/guide/layers.htm#GUID-836DF96B-3821-4051-9A6C-263097CDB86F)

- map view 表现 map 的内容并控制用户如何浏览以及用户和 map 的交互。诸如旋转、平移、缩放之类的操作，且允许用户改变 map 的 viewpoint。map view 可以在 map 上覆盖图表，用以显示如查询或分析的结果。map view 将显示坐标同地图坐标转换，所以你的 app 可以将用户的操作同地图坐标联系起来。

ArcGIS Runtime 提供 map 和 map view 对象，你可以用来 [build new maps](https://developers.arcgis.com/android/latest/guide/build-a-new-map.htm)、[display maps](https://developers.arcgis.com/android/latest/guide/display-a-map.htm)、[save maps](https://developers.arcgis.com/android/latest/guide/save-a-map.htm) 和 [share maps](https://developers.arcgis.com/android/latest/guide/share-a-portal-item.htm)。更多见 [API reference](https://developers.arcgis.com/android/api-reference/index.html)。

> 笔记：
> - 当你在 map 中查看或分析来自不同层或地图源的空间数据时，你可能需要考虑他们的空间引用。更多细节，见 [Spatial references](https://developers.arcgis.com/android/latest/guide/spatial-references.htm#GUID-A316A533-933F-4C92-BF17-732A585B1358)
> - 对象可以在 map 上符号化，它可以来自持久存储的数据（要素数据，如地理数据库中的道路和区域）和临时数据（图文，比如来自 web socket 的数据）。更多细节，见 [Features and graphics](https://developers.arcgis.com/android/latest/guide/features-and-graphics.htm#GUID-663BC99D-18AC-4F15-9ACA-CFE17BEE2315) 以及 [Symbols and renderers](https://developers.arcgis.com/android/latest/guide/symbols-and-renderers.htm)。

# 在线 map
ArcGIS 包括 [Living Atlas of the World](http://doc.arcgis.com/en/living-atlas/)，它有涵盖数千个主题的美丽且权威的地图。从 Esri 以及数千其它组织上探寻 map 和数据，然后将其与你自己的数据结合来创造一个新的 map 和应用。

你在 ArcGIS Online 的 [map viewer](http://www.arcgis.com/home/webmap/viewer.html?useExisting=1) 创建的地图是可以显示地理信息的交互式地图，它可以用来讲述故事和回答问题。这些在线地图可供广泛的受众使用，且包括多尺度的底图、针对特定受众的层，以及一些弹出信息，这些弹出信息允许用户深入他们感兴趣的特定功能。它还支持可视化、编辑、分析和时间。在线 map 可在各种客户端上查看，包括移动 app，桌面 app，web 浏览器。为创建一个在线 map，可以依据 ArcGIS Online Help [get started with maps](http://server.arcgis.com/en/portal/latest/use/get-started-with-maps.htm) 主题中的步骤进行。

你可以从 ArcGIS Online 或其它组织的入口 [create maps](http://server.arcgis.com/en/portal/10.4/use/get-started-with-maps.htm)、[share maps](https://doc.arcgis.com/en/arcgis-online/share-maps/share-items.htm)，以及向你的 app 中加载 map。

# 离线 map

为用户可以离线操作他们的地图，这里有两种模式。[Services pattern](https://developers.arcgis.com/android/latest/guide/maps.htm#ESRI_SECTION2_F7139EB000BF4003AAB390BAF0E7382D) 指 API 自己将地图离线；[Desktop pattern](https://developers.arcgis.com/android/latest/guide/maps.htm#ESRI_SECTION2_297C1CF6CA6C4243B8AB2D924B185A82) 指 你使用额外的工具，如 ArcGIS Pro 来创建移动地图包，让你可以离线使用。更多细节，见 [Offline](https://developers.arcgis.com/android/latest/guide/offline.htm)。

## 服务模式（Services patterns）
服务模式允许你创建的 app 将地图和其层离线任意长的时间，只要你已被[授予离线使用](https://doc.arcgis.com/en/arcgis-online/create-maps/take-maps-offline.htm)。如果你想编辑要素数据（feature data）并在网络恢复时同步更改，你还需要在要素层（feature layers）上[启用同步功能](http://server.arcgis.com/en/portal/latest/use/enable-offline-mapping.htm#guid-a2390dd3-314b-4c81-8a46-08e587748408guid-47abcd3c-af06-414a-8eda-7c38bfa90aba)。该 API 向你提供了两种主要的服务模式：
- 事先生成离线地图，野外工作者只要简单地下载即可使用。参见：[preplanned offline workflow](https://developers.arcgis.com/android/latest/guide/offline.htm#ESRI_SECTION2_5BBF9A50658D4C44A7BB697767B3C558)。
- 如果你的野外工作者需要自定义感兴趣的区域后生成离线地图再下载到设备，参见：[on-demand offline workflow](https://developers.arcgis.com/android/latest/guide/offline.htm#ESRI_SECTION2_C5B94265E94740B5A8FDE79A0DD6042C)。

你还可以离线各个层和数据，然后在 app 中构建地图。这提供了更灵活的层结合方式，参见：[create offline layers](https://developers.arcgis.com/android/latest/guide/create-an-offline-layer.htm)。

## 桌面模式（Desktop pattern）

该模式允许你将地图下载到移动地图包文件（mobile map package file），然后将其分片下载到用户设备。这种方法的优势在于你可以创建一个移动地图包，然后将它分发到许多设备上。这是种“只读”选项，因为你用户做的任何编辑都不能同步到原始的数据源上。

通过 ArcGIS Pro 你可以创建移动地图包，它可以将你组织的地图、资源、道路网络、定位器（locator）包含到一个文件中。更多细节，见 ArcGIS Pro 帮助的 [Mobile map package](http://pro.arcgis.com/en/pro-app/help/sharing/overview/mobile-map-package.htm)。你还可以用 ArcGIS Desktop 创建各个层的包。更多细节，见 [Create an offline layer](https://developers.arcgis.com/android/latest/guide/create-an-offline-layer.htm#ESRI_SECTION1_B8AE19595B964EFEB8180400E873D403) 的桌面模式部分。

> 笔记：
>
> 如果你希望在离线地图（包括定位器和网络数据集）中随时使用并定期更新街道地图，请参阅 [Add StreetMap Premium data](https://developers.arcgis.com/android/latest/guide/add-streetmap-premium-data.htm)。

 






















