---
title: 目錄位置 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog position
- catalog position [ODBC]
ms.assetid: 5bc5f64b-c75a-43d2-8745-102ec7a49000
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0305d978dc4ecd21892a0be3916fa5072b7be95a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303379"
---
# <a name="catalog-position"></a>目錄位置
識別碼中的目錄名稱位置，以及與其余識別碼分隔的方式會因數據源而異。 例如，在 Xbase 資料來源中，目錄名稱是目錄，而在 Microsoft® Windows®中，會以反斜線（\\）分隔資料表名稱（也就是檔案名）。 下圖將示範這種情況。  
  
 ![目錄位置：Xbase](../../../odbc/reference/develop-app/media/ch0801.gif "ch0801")  
  
 在 SQL Server 資料來源中，目錄是資料庫，並以句點（.）分隔架構和資料表名稱。  
  
 ![目錄位置：SQL Server](../../../odbc/reference/develop-app/media/ch0802.gif "ch0802")  
  
 在 Oracle 資料來源中，目錄也是資料庫，但會遵循資料表名稱，並以 @ 符號分隔架構和資料表名稱。  
  
 ![目錄位置：Oracle](../../../odbc/reference/develop-app/media/ch0803.gif "ch0803")  
  
 為了決定目錄分隔符號和目錄名稱的位置，應用程式會使用 SQL_CATALOG_NAME_SEPARATOR 和 SQL_CATALOG_LOCATION 選項來呼叫**SQLGetInfo** 。 互通的應用程式應該根據這些值來建立識別碼。  
  
 將包含多個部分的識別碼加上引號時，應用程式必須謹慎地分別括住每個部分，而不是括住識別碼的字元。 例如，下列語句選取 Xbase 資料表的所有資料列和資料行時，會將目錄（\XBASE\SALES\CORP）和資料表（Parts）名稱加上引號，而不是目錄分隔符號（\\）：  
  
```  
SELECT * FROM "\XBASE\SALES\CORP"\"PARTS.DBF"  
```  
  
 下列語句可選取 Oracle 資料表的所有資料列和資料行，加上引號目錄（銷售）、架構（公司）和資料表（部分）名稱，但不加上目錄（@）或架構（.）分隔符號：  
  
```  
SELECT * FROM "Corporate"."Parts"@"Sales"  
```  
  
 如需引號識別碼的詳細資訊，請參閱下一節的[引號識別碼](../../../odbc/reference/develop-app/quoted-identifiers.md)。
