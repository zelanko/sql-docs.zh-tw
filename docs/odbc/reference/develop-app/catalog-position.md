---
title: 目錄位置 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog position
- catalog position [ODBC]
ms.assetid: 5bc5f64b-c75a-43d2-8745-102ec7a49000
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 160fe63d75439c668263fccaef12f4cf047704f7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32910003"
---
# <a name="catalog-position"></a>目錄位置
識別項和分隔識別碼的其他方式中的目錄名稱位置到資料來源不同資料來源。 比方說，Xbase 資料來源中的目錄名稱是一個目錄，在 Microsoft® Windows®，資料表名稱 （這是檔案名稱） 來隔開反斜線 (\\)。 下圖示範這種狀況。  
  
 ![目錄位置： Xbase](../../../odbc/reference/develop-app/media/ch0801.gif "ch0801")  
  
 在 SQL Server 資料來源、 目錄是資料庫，並以句號 （.） 隔開的結構描述和資料表名稱。  
  
 ![目錄位置： SQL Server](../../../odbc/reference/develop-app/media/ch0802.gif "ch0802")  
  
 在 Oracle 資料來源，目錄也是資料庫，但會遵循資料表名稱，並分開的結構描述和資料表名稱的 @ 記號 (@)。  
  
 ![目錄位置： Oracle](../../../odbc/reference/develop-app/media/ch0803.gif "ch0803")  
  
 若要判斷目錄分隔符號和目錄名稱的位置，應用程式呼叫**SQLGetInfo**與 SQL_CATALOG_NAME_SEPARATOR 和 SQL_CATALOG_LOCATION 選項。 互通的應用程式應該建構根據這些值的識別項。  
  
 用引號括住包含多個組件的識別項，當應用程式必須分別將每個部分加上引號及不加上引號分隔識別碼的字元，請小心。 例如，下列陳述式，即可選取所有資料列和 Xbase 資料表的資料行引號 (\XBASE\SALES\CORP) 的類別目錄和資料表 (Parts.dbf) 名稱，但不是目錄分隔符號 (\\):  
  
```  
SELECT * FROM "\XBASE\SALES\CORP"\"PARTS.DBF"  
```  
  
 下列陳述式，選取所有資料列和資料行，Oracle 資料表的引號目錄 (Sales)、 結構描述 （「 公司 」），和資料表 （部分） 名稱，但不是類別目錄 (@) 或結構描述 （.） 分隔：  
  
```  
SELECT * FROM "Corporate"."Parts"@"Sales"  
```  
  
 引號識別項的相關資訊，請參閱下節中，[引號識別項](../../../odbc/reference/develop-app/quoted-identifiers.md)。
