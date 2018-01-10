参见：[Maps(2D)](https://developers.arcgis.com/android/latest/guide/maps.htm)

- [概述](#%E6%A6%82%E8%BF%B0)
- [在线 map](#%E5%9C%A8%E7%BA%BF-map)
- [离线 map](#%E7%A6%BB%E7%BA%BF-map)

# 概述

地图可以讲述故事、体现想法或展示情况。 它可以帮助你完成数以百计事，从查找最近的医院到观看与人口密集地区有关的地震事件。

不像大多数 map，ArcGIS map 有许多额外的功能。它们可以包含由层组织的数据且拥有分析能力，能让你发现模式并解决许多类型的问题。例如，一个 ArcGIS map 可以向你展示一卡车队在某区域内的移动，且它可以优化它们的路径来最大化车队效率。

一个 map 通常由提供地理环境的 basemap 和包含 map 重要内容的操作层组成。你可以在你的 app map 内使用你自己的数据，Esri 的数据，或两者混合。在 ArcGIS Runtime app，map 可以和 map view 一起使用来在屏幕上显示地理数据。在这种情况下，map 作为 MVC 架构中的 model 层，map view 作为 view 层：

- map 指定了地理内容（数据）来自哪里且应该如何组织（它有哪些层，什么 bookmark，初始 viewpoint 等）。各层的内容可能来自各种各样的[地图源](https://developers.arcgis.com/android/latest/guide/maps.htm#ESRI_SECTION1_FC86B8F7930B4D6C91484EBC7F381CFB)，包括在线的数据源或本地存储的数据，例如移动地理数据库中的功能表或移动地图包中的数据。更多关于你可以包含进 map 的数据和层类型，见 [Layers and tables](https://developers.arcgis.com/android/latest/guide/layers.htm#GUID-836DF96B-3821-4051-9A6C-263097CDB86F)
- map view 表现 map 的内容并控制用户如何浏览以及用户和 map 的交互。诸如旋转、平移、缩放之类的操作允许用户改变 map 的 viewpoint。map view 可以在 map 上覆盖图表，用以显示如查询或分析的结果。map view 将显示坐标同地图坐标转换，所以你的 app 可以将用户的操作同地图坐标联系起来。

ArcGIS Runtime 提供 map 和 map view 对象，你可以用来 [build new maps](https://developers.arcgis.com/android/latest/guide/build-a-new-map.htm)、[display maps](https://developers.arcgis.com/android/latest/guide/display-a-map.htm)、[save maps](https://developers.arcgis.com/android/latest/guide/save-a-map.htm) 和 [share maps](https://developers.arcgis.com/android/latest/guide/share-a-portal-item.htm)。更多见 [API reference](https://developers.arcgis.com/android/api-reference/index.html)。

> 笔记：
> - 当你在 map 中查看或分析来自不同层或地图源的空间数据时，你可能需要考虑他们的空间引用。更多细节，见 [Spatial references](https://developers.arcgis.com/android/latest/guide/spatial-references.htm#GUID-A316A533-933F-4C92-BF17-732A585B1358)
> - 对象可以在 map 上符号化，它可以来自持久数据（特征数据，如地理数据库中的道路和区域）和临时数据（图文，比如来自 web socket 的数据）。更多细节，见 [Features and graphics](https://developers.arcgis.com/android/latest/guide/features-and-graphics.htm#GUID-663BC99D-18AC-4F15-9ACA-CFE17BEE2315) 以及 [Symbols and renderers](https://developers.arcgis.com/android/latest/guide/symbols-and-renderers.htm)。

# 在线 map
ArcGIS 包括 [Living Atlas of the World](http://doc.arcgis.com/en/living-atlas/)，它有涵盖数千个主题的美丽且权威的地图。从 Esri 以及数千其它组织上探寻 map 和数据，然后将其与你自己的数据结合来创造一个新的 map 和应用。

你在 ArcGIS Online 的 [map viewer](http://www.arcgis.com/home/webmap/viewer.html?useExisting=1) 创建的地图是交互式地图，可以显示地理信息来讲述故事和回答问题。这些在线地图可供广泛的受众使用，且包括多尺度的 basemap，针对特定受众的层，以及允许用户深入他们感兴趣的特定功能的弹出信息。它还支持可视化、编辑、分析和时间。在线 map 可在各种客户端上查看，包括移动 app，桌面 app，web 浏览器。为创建一个在线 map，可以依据 ArcGIS Online Help [get started with maps](http://server.arcgis.com/en/portal/latest/use/get-started-with-maps.htm) 主题中的步骤进行。

你可以从 ArcGIS Online 或其它组织的入口 [create maps](http://server.arcgis.com/en/portal/10.4/use/get-started-with-maps.htm)、[share maps](https://doc.arcgis.com/en/arcgis-online/share-maps/share-items.htm)，以及向你的 app 中加载 map。

# 离线 map






















