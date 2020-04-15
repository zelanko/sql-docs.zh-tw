---
title: 建立連接 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6f71190a8a2ca1dd8af0d28adb5531540fb1b57e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298698"
---
# <a name="establishing-a-connection"></a>建立連線
在分配環境和連接句柄並設置任何連接屬性後,應用程式已準備好連接到數據源或驅動程式。 應用程式可以使用三種不同的功能 **:SQLConnect(** 核心介面一致性級別 **)、SQLDriverConnect(** 核心)和**SQLBrowseConnect(** 級別 1)。 這三者中的每一個都設計為在不同的場景中使用。 在連接之前,應用程式可以確定 SQLDrivers 返回的**ConnectFunctions**關鍵字支援這些函數中的**哪一**個。  
  
> [!NOTE]  
>  某些驅動程式限制其支援的活動連接數。 應用程式使用SQL_MAX_DRIVER_CONNECTIONS選項調用**SQLGetInfo,** 以確定特定驅動程式支援多少活動連接。  
  
 此章節包含下列主題。  
  
-   [預設資料來源](../../../odbc/reference/develop-app/default-data-source.md)  
  
-   [使用 SQLConnect 進行連線](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)  
  
-   [連接字串](../../../odbc/reference/develop-app/connection-strings.md)  
  
-   [使用 SQLDriverConnect 進行連線](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)  
  
-   [使用 SQLDriverConnect 進行連線](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)
