---
title: 使用 sqldriverconnect 進行連接 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 78cdaabe867ae67e3a1dfcb80e82cfaf95a94ed1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47797906"
---
# <a name="connecting-with-sqldriverconnect"></a>使用 SQLDriverConnect 進行連線
**SQLDriverConnect**用來連接到資料來源使用的連接字串。 **SQLDriverConnect**而非**SQLConnect** ，原因如下：  
  
-   若要讓應用程式使用驅動程式特有的連接資訊。  
  
-   要求驅動程式提示使用者輸入連接資訊。  
  
-   若要連線時未指定資料來源。  
  
 此章節包含下列主題。  
  
-   [特定驅動程式的連接資訊](../../../odbc/reference/develop-app/driver-specific-connection-information.md)  
  
-   [提示使用者輸入連接資訊](../../../odbc/reference/develop-app/prompting-the-user-for-connection-information.md)  
  
-   [使用檔案資料來源進行連接](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)  
  
-   [直接連接到驅動程式](../../../odbc/reference/develop-app/connecting-directly-to-drivers.md)
