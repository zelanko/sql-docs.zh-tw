---
title: 目錄位置 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303379"
---
# <a name="catalog-position"></a>目錄位置
目錄名稱在標識符中的位置以及它與標識符的其餘部分的分離方式因數據源而異。 例如,在 Xbase 資料來源中,目錄名稱是目錄,在 Microsoft 中® Windows®,由\\反斜杠 () 與表名(檔名)分隔。 下圖演示了此條件。  
  
 ![目錄位置：Xbase](../../../odbc/reference/develop-app/media/ch0801.gif "ch0801")  
  
 在 SQL Server 資料來源中,目錄是資料庫,與架構和表名分隔了一個句點 (.)。  
  
 ![目錄位置：SQL Server](../../../odbc/reference/develop-app/media/ch0802.gif "ch0802")  
  
 在 Oracle 資料來源中,目錄也是資料庫,但遵循表名稱,並由 at a 符號 (*) 與架構和表名稱分開。  
  
 ![目錄位置：Oracle](../../../odbc/reference/develop-app/media/ch0803.gif "ch0803")  
  
 要確定目錄分隔符和目錄名稱的位置,應用程式使用SQL_CATALOG_NAME_SEPARATOR和SQL_CATALOG_LOCATION選項調用**SQLGetInfo。** 可互通的應用程式應根據這些值構造標識碼。  
  
 在引用包含多個部件的標識符時,應用程式必須小心單獨報價每個部件,而不是引用分隔標識符的字元。 例如,以下文句用於選擇 Xbase 表的所有行和列,引用目錄 (_XBASE_SALES_CORP) 和表 (parts.dbf) 名稱,但不\\包括目錄分隔符 ( ):  
  
```  
SELECT * FROM "\XBASE\SALES\CORP"\"PARTS.DBF"  
```  
  
 以下用於選擇 Oracle 表的所有行和列的語句引用目錄(銷售)、架構(公司)和表(部件)名稱,但參考目錄 (+) 或架構 (.) 分隔符:  
  
```  
SELECT * FROM "Corporate"."Parts"@"Sales"  
```  
  
 有關報價標識符的資訊,請參閱下一節[「引用標識符](../../../odbc/reference/develop-app/quoted-identifiers.md)」。
