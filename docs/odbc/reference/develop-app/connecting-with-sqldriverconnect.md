---
title: 使用 SQLDriverConnect 連線 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- functions [ODBC], data source or driver connections
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- SQLDriverConnect function [ODBC], connecting
- connection functions [ODBC]
- ODBC drivers [ODBC], connection functions
ms.assetid: e46e959f-d3c5-4ddb-810a-107bfcb83fd2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6cd95364d8a5316a50d9f55616236a8677bf99e4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299068"
---
# <a name="connecting-with-sqldriverconnect"></a>使用 SQLDriverConnect 進行連線
**SQLDriverConnect**用於使用連接字串連接到數據源。 **SQLDriverConnect**的使用而不是**SQLConnect,** 原因如下:  
  
-   讓應用程式使用特定於驅動程式的連接資訊。  
  
-   要求驅動程式提示使用者輸入連接資訊。  
  
-   在不指定數據源的情況下進行連接。  
  
 此章節包含下列主題。  
  
-   [特定驅動程式的連線資訊](../../../odbc/reference/develop-app/driver-specific-connection-information.md)  
  
-   [提示使用者輸入連線資訊](../../../odbc/reference/develop-app/prompting-the-user-for-connection-information.md)  
  
-   [使用檔案資料來源進行連線](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)  
  
-   [直接連線到驅動程式](../../../odbc/reference/develop-app/connecting-directly-to-drivers.md)
