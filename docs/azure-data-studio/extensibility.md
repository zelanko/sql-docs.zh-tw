---
title: 透過擴充性新增其他功能
titleSuffix: Azure Data Studio
description: 了解用於擴充 Azure Data Studio 功能的擴充性模型和重要擴充性領域
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: b263c3890ab9a03295212c723adad4a431fbf04f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "76928003"
---
# <a name="getting-started-with-includename-sosincludesname-sos-shortmd-extensibility"></a>開始使用 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 擴充性

[!INCLUDE[name-sos](../includes/name-sos.md)] 具有數個擴充性機制，可自訂使用者體驗，並將這些自訂項目提供給整個使用者社群。 核心 [!INCLUDE[name-sos](../includes/name-sos.md)] 平台是以 Visual Studio Code 為建置基礎，因此大部分的 Visual Studio Code 擴充性 API 都可供使用。 此外，我們也為資料管理特定活動提供了額外的擴充點。

其中一些重要的擴充點包括：

- Visual Studio Code 擴充性 API
- Azure Data Studio 延伸模組撰寫工具
- 管理儀表板索引標籤面板貢獻
- 可採取動作的深入解析體驗
- Azure Data Studio 擴充性 API
- 自訂 Data Provider API

## <a name="visual-studio-code-extensibility-apis"></a>Visual Studio Code 擴充性 API

由於核心 [!INCLUDE[name-sos](../includes/name-sos.md)] 平台是以 Visual Studio Code 為建置基礎，因此您可以在 Visual Studio Code 網站的[延伸模組撰寫](https://code.visualstudio.com/docs/extensions/overview)和[延伸模組 API](https://code.visualstudio.com/docs/extensionAPI/overview) 文件中，找到 Visual Studio Code 擴充性 API 的詳細資料。

## <a name="manage-dashboard-tab-panel-contributions"></a>管理儀表板索引標籤面板貢獻

如需詳細資訊，請參閱[貢獻點](#contribution-points)和[內容變數](#context-variables)。

## <a name="azure-data-studio-extensibility-apis"></a>Azure Data Studio 擴充性 API

如需詳細資訊，請參閱[擴充性 API](extensibility-apis.md)。


## <a name="contribution-points"></a>貢獻點

本節涵蓋 package.json 延伸模組資訊清單中定義的各種貢獻點。

azuredatastudio 中支援 IntelliSense。

## <a name="contributes-dashboard"></a>提供給儀表板

將索引標籤、容器、深入解析小工具提供給儀表板。

![儀表板](media/extensibility/dashboard-page.png)

`dashboard.tabs`

Dashboard.tabs 會在儀表板頁面內建立索引標籤區段。 其中必須有物件或物件陣列。  

```json
"dashboard.tabs": [
{
    "id": "test-tab1",
    "title": "Test 1",
    "description": "The test 1 displays a list of widgets.",
    "when": "connectionProvider == 'MSSQL' && !mssql:iscloud",
    "alwaysShow": true,
    "container": {
        ...
    }
}
]
```

`dashboard.containers`

不需要指定內嵌儀表板容器 (在 dashboard.tab 內)。 您可以使用 dashboard.containers 註冊容器。 它接受物件或物件陣列。

```json
"dashboard.containers": [
{
    "id": "innerTab1",
    "container": {
        ...
    }
},
{
    "id": "innerTab2",
    "container": {
       ...
    }
}
]
```

若要參考已註冊的容器，請指定容器的識別碼

```json
"dashboard.tabs": [
{
    ...
    "container": {
        "innerTab1": {             
        }
    }
}
]

```

`dashboard.insights`

您可以使用 dashboard.insights 註冊深入解析。 這類似[教學課程：建置自訂深入解析小工具](https://docs.microsoft.com/sql/sql-operations-studio/tutorial-build-custom-insight-sql-server)

```json
"dashboard.insights": {
"id": "my-widget"
"type": {
    "count": {
        "dataDirection": "vertical",
        "dataType": "number",
        "legendPosition": "none",
           "labelFirstColumn": false,
        "columnsAsLabels": false
       }
   },
   "queryFile": "{your file folder}/activeSession.sql"
}
```


### <a name="dashboard-container-types"></a>儀表板容器類型

目前支援四種容器類型：

1. `widgets-container`

    ![widgets-container](media/extensibility/widgets-container.png)

    小工具清單會顯示在容器中。 這是流程配置。 它接受小工具清單。

    ```json
    "container": {
        "widgets-container": [
        {
            "widget": {
                "query-data-store-db-insight": {
                }
            }
        },
        {
            "widget": {
                "explorer-widget": {
                }
            }
        }
      ]
    }
    ```

2. `webview-container`

    ![webview-container](media/extensibility/webview-container.png)

    WebView 會顯示在整個容器中。 WebView 識別碼必須與索引標籤識別碼相同

    ```json
    "container": {
        "webview-container": null
    }
    ```

3. `grid-container`

   ![grid-container](media/extensibility/grid-container.png)

   會顯示在格線配置中的小工具或 WebView 清單

    ```json
    "container": {
        "grid-container": [
        {
            "name": "widget 1",
            "widget": {
                "explorer-widget": {
                }
            },
            "row":0,
            "col":0
        },
        {
            "name": "widget 2",
            "widget": {
                "tasks-widget": {
                    "backup", 
                    "restore",
                    "configureDashboard",
                    "newQuery"
                }
            },
            "row":0,
            "col":1
        },
        {
            "name": "Webview 1",
            "webview": {
                "id": "google"
            },
            "row":1,
            "col":0,
            "colspan":2
        },
        {
            "name": "widget 3",
            "widget": {
                "explorer-widget": {}
            },
            "row":0,
            "col":3,
            "rowspan":2
        },
    ]
    ```

4.  `nav-section`

    ![nav-section](media/extensibility/nav-section.png)

    導覽區段會顯示在容器中

    ```json
    "container": {
        "nav-section": [
            {
                "id": "innerTab1",
                "title": "inner-tab1",
                "icon": {
                    "light": "./icons/tab1Icon.svg",
                    "dark": "./icons/tab1Icon_dark.svg"
                }
                "container": {
                    ...
                }
            },
            {
                "id": "innerTab2",
                "title": "inner-tab2",
                "icon": {
                    "light": "./icons/tab2Icon.svg",
                    "dark": "./icons/tab2Icon_dark.svg"
                }
                "container": {
                    ...
                }
            }
        ]
    }
    ```



## <a name="context-variables"></a>內容變數

如需 Visual Studio Code 和後續 Azure Data Studio 中內容的一般資訊，請參閱[擴充性](https://code.visualstudio.com/docs/extensionAPI/extension-points#_example)。

在 Azure Data Studio 中，我們有資料庫連線 (可用於延伸模組) 的相關特定內容。

### <a name="dashboard"></a>儀表板

在儀表板中，我們提供下列內容變數：

|內容變數| description|
|:---|:---|
|`connectionProvider` | 目前連線提供者的識別碼字串。 例如 第 1 課：建立 Windows Azure 儲存體物件`connectionProvider == 'MSSQL'`。|
|`serverName`|目前連線的伺服器名稱字串。 例如 第 1 課：建立 Windows Azure 儲存體物件`serverName == 'localhost'`。|
|`databaseName` | 目前連線的資料庫名稱字串。 例如 第 1 課：建立 Windows Azure 儲存體物件`databaseName == 'master'`。|
|`connection` | 目前連線的完整連線設定檔物件 (IConnectionProfile)|
|`dashboardContext` | 目前所在的儀表板頁面內容字串。 可能是 'database' 或 'server'。 例如 `dashboardContext == 'database'`|
