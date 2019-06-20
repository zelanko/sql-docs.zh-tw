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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 22a9a9d50891a6101076af6378fb33543274b21b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63237923"
---
# <a name="catalog-position"></a>目錄位置
目錄名稱識別項和如何分隔識別碼的其餘部分中的位置到資料來源不同資料來源。 比方說，Xbase 資料來源中的目錄名稱是一個目錄，在 Microsoft® Windows®，為分開的資料表名稱 （這是檔案名稱） 反斜線 (\\)。 下圖示範這種情況。  
  
 ![目錄位置：Xbase](../../../odbc/reference/develop-app/media/ch0801.gif "ch0801")  
  
 在 SQL Server 資料來源中，目錄是資料庫，並以句號 （.） 隔開的結構描述和資料表名稱。  
  
 ![目錄位置：SQL Server](../../../odbc/reference/develop-app/media/ch0802.gif "ch0802")  
  
 Oracle 資料來源，在類別目錄也是資料庫，但會遵循資料表名稱和分開的結構描述和資料表名稱的 @ 記號 (@)。  
  
 ![目錄位置：Oracle](../../../odbc/reference/develop-app/media/ch0803.gif "ch0803")  
  
 若要判斷目錄分隔符號，以及目錄名稱的位置，應用程式會呼叫**SQLGetInfo**使用 SQL_CATALOG_NAME_SEPARATOR 和 SQL_CATALOG_LOCATION 選項。 互通的應用程式應該建構根據這些值的識別碼。  
  
 當加註引號於含有多個組件之識別項，應用程式必須非常小心分別將每個部分加上引號，並不加上引號來分隔識別碼的字元。 比方說，下列陳述式，以選取所有資料列和 Xbase 資料表資料行的引號目錄 (\XBASE\SALES\CORP) 和資料表 (Parts.dbf) 名稱，但不是目錄分隔符號 (\\):  
  
```  
SELECT * FROM "\XBASE\SALES\CORP"\"PARTS.DBF"  
```  
  
 下列陳述式，選取所有資料列和資料行，Oracle 資料表的引號目錄 (Sales)、 結構描述 （「 公司 」），以及資料表 （部分） 名稱，但不是類別目錄 (@) 或結構描述 （.） 分隔：  
  
```  
SELECT * FROM "Corporate"."Parts"@"Sales"  
```  
  
 引號識別項的相關資訊，請參閱下一步 區段中，[加上引號的識別項](../../../odbc/reference/develop-app/quoted-identifiers.md)。
