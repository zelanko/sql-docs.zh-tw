---
description: 目錄位置
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
ms.openlocfilehash: 513c2449d296d167c499942636cbb94d637a2ede
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465960"
---
# <a name="catalog-position"></a>目錄位置
目錄名稱在識別碼中的位置，以及與其余識別碼分隔的方式，會因數據源而異。 例如，在 Xbase 資料來源中，目錄名稱是目錄，而在 Microsoft® Windows®中，則是以資料表名稱分隔， (也就是反斜線 () ) 的檔案名 \\ 。 下圖將示範這種情況。  
  
 ![目錄位置：Xbase](../../../odbc/reference/develop-app/media/ch0801.gif "ch0801")  
  
 在 SQL Server 資料來源中，目錄是一種資料庫，並以句點 (. ) 來分隔架構和資料表名稱。  
  
 ![目錄位置：SQL Server](../../../odbc/reference/develop-app/media/ch0802.gif "ch0802")  
  
 在 Oracle 資料來源中，目錄也是資料庫，但會在資料表名稱之後，並以 @ ) 的 @ 符號 ( @ 分隔。  
  
 ![目錄位置：Oracle](../../../odbc/reference/develop-app/media/ch0803.gif "ch0803")  
  
 為了判斷目錄分隔符號和目錄名稱的位置，應用程式會使用 SQL_CATALOG_NAME_SEPARATOR 和 SQL_CATALOG_LOCATION 選項來呼叫 **SQLGetInfo** 。 互通的應用程式應該根據這些值來建立識別碼。  
  
 當您將包含多個部分的識別碼加上引號時，應用程式必須小心地為每個部分加上引號，而不是用來括住識別碼的分隔字元。 例如，若要選取 Xbase 資料表的所有資料列和資料行，請使用下列語句來括住目錄 ( \XBASE\SALES\CORP) 和資料表 (部分 .dbf) 名稱，但不是目錄分隔符號 (\\) ：  
  
```  
SELECT * FROM "\XBASE\SALES\CORP"\"PARTS.DBF"  
```  
  
 下列語句可選取 Oracle 資料表的所有資料列和資料行， (Sales) 、架構 (公司) 和資料表 (部分) 名稱，但不是目錄 ( @ ) 或架構 (。 ) 分隔符號：  
  
```  
SELECT * FROM "Corporate"."Parts"@"Sales"  
```  
  
 如需引號識別碼的詳細資訊，請參閱下一節的 [引號識別碼](../../../odbc/reference/develop-app/quoted-identifiers.md)。
