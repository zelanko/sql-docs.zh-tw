---
title: "使用 SQLDriverConnect 連接 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f918c4f5b32f913fea3d48b05c24c1070fe8f4ef
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="connecting-with-sqldriverconnect"></a>使用 SQLDriverConnect 的連接
**SQLDriverConnect**用來連接到資料來源使用的連接字串。 **SQLDriverConnect**而非**SQLConnect** ，原因如下：  
  
-   若要讓應用程式使用驅動程式特有的連接資訊。  
  
-   要求驅動程式提示使用者輸入連接資訊。  
  
-   若要連接卻未指定資料來源。  
  
 此章節包含下列主題。  
  
-   [特定驅動程式的連接資訊](../../../odbc/reference/develop-app/driver-specific-connection-information.md)  
  
-   [提示使用者輸入連接資訊](../../../odbc/reference/develop-app/prompting-the-user-for-connection-information.md)  
  
-   [使用檔案資料來源進行連接](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)  
  
-   [直接連接到驅動程式](../../../odbc/reference/develop-app/connecting-directly-to-drivers.md)
