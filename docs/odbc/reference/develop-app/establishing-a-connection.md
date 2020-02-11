---
title: 建立連接 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- SQLBrowseConnect function [ODBC], establishing a connection
- functions [ODBC], data source or driver connections
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- connection functions [ODBC]
- SQLConnect function [ODBC], establishing a connection
- SQLDriverConnect function [ODBC], making a connection
- ODBC drivers [ODBC], connection functions
ms.assetid: 8e3c717e-35e3-47ef-b5d3-3a96eeb7b869
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7ef6f3d50382d810dd9df246c4d857d9467674f2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "76941029"
---
# <a name="establishing-a-connection"></a>建立連線
在配置環境和連接控制碼並設定任何連接屬性之後，應用程式就已準備好連接到資料來源或驅動程式。 應用程式可以使用三種不同的功能來執行這項操作： **SQLConnect** （核心介面一致性層級）、 **SQLDriverConnect** （核心）和**SQLBrowseConnect** （層級1）。 這三個都是設計成在不同的案例中使用。 連接之前，應用程式可以使用**SQLDrivers**所傳回的**ConnectFunctions**關鍵字來判斷支援哪些函式。  
  
> [!NOTE]  
>  某些驅動程式會限制其支援的作用中連線數目。 應用程式會使用 SQL_MAX_DRIVER_CONNECTIONS 選項呼叫**SQLGetInfo** ，以判斷特定驅動程式支援的作用中連接數目。  
  
 此章節包含下列主題。  
  
-   [預設資料來源](../../../odbc/reference/develop-app/default-data-source.md)  
  
-   [使用 SQLConnect 進行連線](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)  
  
-   [連接字串](../../../odbc/reference/develop-app/connection-strings.md)  
  
-   [使用 SQLDriverConnect 進行連線](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)  
  
-   [使用 SQLDriverConnect 進行連線](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)
