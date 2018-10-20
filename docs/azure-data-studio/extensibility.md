---
title: 延伸 Azure Data Studio 的功能 | Microsoft Docs
description: 了解有關擴充 Azure Data Studio
ms.custom: tools|sos
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d218f80067c3dd5a03ced864b815c68aa84a582e
ms.sourcegitcommit: ef78cc196329a10fc5c731556afceaac5fd4cb13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2018
ms.locfileid: "49460243"
---
# <a name="getting-started-with-includename-sosincludesname-sos-shortmd-extensibility"></a>開始使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]擴充性

[!INCLUDE[name-sos](../includes/name-sos.md)] 有數個擴充性機制，以自訂使用者體驗，以及讓整個使用者社群中使用這些自訂。 核心[!INCLUDE[name-sos](../includes/name-sos.md)]平台會根據 Visual Studio Code 中，因此大部分的 Visual Studio Code 擴充性 Api 可使用。 此外，我們提供了額外的擴充性點的資料特定管理活動。

金鑰的擴充性點的部分包括：

- Visual Studio Code 擴充性 Api
- Azure 製作工具的資料 Studio 擴充功能
- 管理儀表板 索引標籤面板的貢獻
- 深入了解動作體驗
- Azure Data Studio 擴充性 Api
- 自訂資料提供者 Api

## <a name="visual-studio-code-extensibility-apis"></a>Visual Studio Code 擴充性 Api

因為核心[!INCLUDE[name-sos](../includes/name-sos.md)]平台會根據 Visual Studio Code、 Visual Studio Code 擴充性 Api 的詳細資料中找到[延伸模組製作](https://code.visualstudio.com/docs/extensions/overview)並[延伸模組 API](https://code.visualstudio.com/docs/extensionAPI/overview)Visual Studio Code 網站上的文件。

## <a name="manage-dashboard-tab-panel-contributions"></a>管理儀表板 索引標籤面板的貢獻

如需詳細資訊，請參閱 <<c0> [ 貢獻點](#contribution-points)並[內容變數](#context-variables)。

## <a name="azure-data-studio-extensibility-apis"></a>Azure Data Studio 擴充性 Api

如需詳細資訊，請參閱 <<c0> [ 擴充性 Api](extensibility-apis.md)。


## <a name="contribution-points"></a>貢獻點

本章節涵蓋 package.json 延伸模組資訊清單中所定義的各種貢獻點。

Azuredatastudio 內，不支援 IntelliSense。

## <a name="contributes-dashboard"></a>提供儀表板

參與索引標籤、 容器、 深入解析儀表板的小工具。

![儀表板](media/extensibility/dashboard-page.png)

`dashboard.tabs`

Dashboard.tabs 建立儀表板頁面內的索引標籤區段。 它預期物件的陣列。  

```json
"dashboard.tabs": [
{
    "id": "test-tab1",
    "title": "Test 1",
    "description": "The test 1 displays a list of widgets.",
    "when": "connectionProvider == 'MSSQL' && !mssql:iscloud",
    "alwaysShow": true,
    "container": {
        …
    }
}
]
```

`dashboard.containers`

而不是指定將容器內嵌儀表板 （位於內部 dashboard.tab)。 您可以註冊使用 dashboard.containers 的容器。 它會接受物件的陣列。

```json
"dashboard.containers": [
{
    "id": "innerTab1",
    "container": {
        …
    }
},
{
    "id": "innerTab2",
    "container": {
       …
    }
}
]
```

若要參考已註冊的容器，指定容器的識別碼

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

您可以註冊使用 dashboard.insights 的深入解析。 這是類似於[教學課程： 建置自訂的深入解析小工具](https://docs.microsoft.com/sql/sql-operations-studio/tutorial-build-custom-insight-sql-server)

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


### <a name="dashboard-container-types"></a>儀表板的容器類型

目前有四種支援的容器類型：

1. `widgets-container`

    ![小工具的容器](media/extensibility/widgets-container.png)

    將容器中顯示的小工具的清單。 這是流程配置。 它可接受小工具的清單。

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

    ![web 檢視容器](media/extensibility/webview-container.png)

    Web 檢視會顯示在整個容器。 它會預期要索引標籤的識別碼也是一樣的 webview 識別碼

    ```json
    "container": {
        "webview-container": null
    }
    ```

3. `grid-container`

   ![方格容器](media/extensibility/grid-container.png)

   Widget 或將會顯示在格線版面配置的 web 檢視的清單

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

    ![瀏覽區段](media/extensibility/nav-section.png)

    瀏覽區段會顯示在容器中

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
                    …
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
                    …
                }
            }
        ]
    }
    ```



## <a name="context-variables"></a>內容變數

如需在 Visual Studio Code 和後續 Azure Data Studio 中的內容的一般資訊，請參閱[擴充性](https://code.visualstudio.com/docs/extensionAPI/extension-points#_example)。

在 Azure Data Studio，我們會有可用的延伸模組的資料庫連接相關的特定內容。

### <a name="dashboard"></a>儀表板

在儀表板，我們會提供下列的內容變數：

|內容變數| description|
|:---|:---|
|`connectionProvider` | 目前連接的提供者的識別項的字串。 例如 `connectionProvider == 'MSSQL'` 。|
|`serverName`|目前連接的伺服器名稱的字串。 例如 `serverName == 'localhost'` 。|
|`databaseName` | 目前連接的資料庫名稱的字串。 例如 `databaseName == 'master'` 。|
|`connection` | 完整的連線設定檔物件，目前的連接 (IConnectionProfile)|
|`dashboardContext` | 儀表板頁面內容的字串，目前已開啟。 'Database' 或者 'server'。 例如 `dashboardContext == 'database'`|
