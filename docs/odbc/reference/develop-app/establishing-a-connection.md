---
title: 建立連線 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
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
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 21b410afda6e5420b723360cdde03cb76f8b7293
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="establishing-a-connection"></a>建立連線
配置環境和連接控制代碼，並設定任何連接屬性，應用程式之後可以連接至資料來源或驅動程式。 有三個不同的函數，應用程式可用來執行這項操作： **SQLConnect** （核心介面的一致性層級） **SQLDriverConnect** （核心），和**SQLBrowseConnect**(層級 1)。 每三個被為了在不同的案例中使用。 連接之前，先在應用程式可以判斷與支援的這些函式**ConnectFunctions**所傳回的關鍵字**SQLDrivers**。  
  
> [!NOTE]  
>  有些驅動程式限制它們支援的作用中連線數目。 應用程式呼叫**SQLGetInfo** SQL_MAX_DRIVER_CONNECTIONS 選項，以決定多少作用中連線的特定驅動程式支援。  
  
 此章節包含下列主題。  
  
-   [預設的資料來源](../../../odbc/reference/develop-app/default-data-source.md)  
  
-   [使用 SQLConnect 進行連接](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)  
  
-   [連接字串](../../../odbc/reference/develop-app/connection-strings.md)  
  
-   [使用 SQLDriverConnect 進行連接](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)  
  
-   [使用 SQLDriverConnect 進行連接](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)
