---
title: 建立連線 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- SQLBrowseConnect function [ODBC], establising a connection
- functions [ODBC], data source or driver connections
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- connection functions [ODBC]
- SQLConnect function [ODBC], establising a connection
- SQLDriverConnect function [ODBC], making a connection
- ODBC drivers [ODBC], connection functions
ms.assetid: 8e3c717e-35e3-47ef-b5d3-3a96eeb7b869
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 70f459f60616e7edd77078a7e9653ab9dff097e9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63248350"
---
# <a name="establishing-a-connection"></a>建立連線
配置環境和連接控制代碼，並設定任何連接屬性，應用程式之後即可連接到資料來源或驅動程式。 有三個不同的函式應用程式可用來執行這項操作：**SQLConnect** （核心介面一致性層級）， **SQLDriverConnect** （核心），以及**SQLBrowseConnect** (層級 1)。 每三個可用於不同的案例。 連線之前，應用程式可以決定其中哪些功能支援**ConnectFunctions**所傳回的關鍵字**SQLDrivers**。  
  
> [!NOTE]  
>  有些驅動程式限制它們支援的作用中連線數目。 應用程式呼叫**SQLGetInfo** SQL_MAX_DRIVER_CONNECTIONS 選項，以決定多少個作用中連線的特定驅動程式支援。  
  
 此章節包含下列主題。  
  
-   [預設的資料來源](../../../odbc/reference/develop-app/default-data-source.md)  
  
-   [使用 SQLConnect 進行連接](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)  
  
-   [連接字串](../../../odbc/reference/develop-app/connection-strings.md)  
  
-   [使用 SQLDriverConnect 進行連接](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)  
  
-   [使用 SQLDriverConnect 進行連接](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)
