---
title: 陳述式參數 |Microsoft 文件
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
- statement parameters [ODBC]
ms.assetid: 58d5b166-2578-4699-a560-1f1e6d86c49a
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3e3c7aa5880c80dff412a69d51cda42d24824e01
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="statement-parameters"></a>陳述式參數
A*參數*是 SQL 陳述式中的變數。 例如，假設零件資料表中具有名為 PartID、 描述和價格的資料行。 若要將組件不含參數需要建構 SQL 陳述式，例如：  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 雖然這個陳述式會插入新的訂單，但是它不是訂單輸入應用程式的最佳解決方案因為要插入之值不能是硬式編碼應用程式中。 替代方法是建構 SQL 陳述式在執行階段，使用要插入的值。 這不也很好的解決方案，因為在執行階段建構陳述式的複雜度。 最好的解決方案是要取代的項目**值**子句以問號 （？），或*參數標記*:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 然後會將參數標記繫結到應用程式變數。 若要加入新的資料列，應用程式必須只設定變數的值，並執行陳述式。 然後驅動程式會擷取目前的變數值，再將其傳送給資料來源。 如果陳述式將會執行多次，應用程式可讓處理程序更有效率預備此陳述式。  
  
 如上所示的陳述式可能是硬式編碼訂單輸入應用程式中插入新資料列。 不過，不一定要垂直應用程式，將參數標記。 任何應用程式，其可簡化在執行階段建構 SQL 陳述式，藉由避免發生的文字轉換的困難度。 比方說，只顯示的組件識別碼可能是儲存在應用程式中的整數。 如果 SQL 陳述式會建構不含參數標記，應用程式必須轉換成文字的組件識別碼和資料來源必須將它轉換回整數。 藉由使用參數標記，應用程式可以部分識別碼傳送至驅動程式通常可以將它傳送至資料來源，以整數形式的整數。 這會儲存兩個轉換。 Long 資料值，這是很重要，因為這類值的文字形式經常會超過 SQL 陳述式的允許的長度。  
  
 只有在 SQL 陳述式中的特定位置參數都有效。 比方說，他們不允許在選取清單中 (要傳回之資料行清單**選取**陳述式)，或是否允許為等號 （=），這類的二元運算子的兩個運算元因為難以判斷參數類型。 一般來說，參數是只在資料操作語言 (DML) 陳述式，而不是在資料定義語言 (DDL) 陳述式時才有效。 如需詳細資訊，請參閱[參數標記](../../../odbc/reference/appendixes/parameter-markers.md)附錄 c: SQL 文法中。  
  
 當 SQL 陳述式會叫用名為參數的程序，可以使用。 具名的參數的名稱，不是由在 SQL 陳述式中的位置來識別。 呼叫所繫結**SQLBindParameter**，但不是由參數識別 IPD （實作參數描述項，） 的 SQL_DESC_NAME 欄位*Sqlbindparameter*引數**SQLBindParameter**。 也可以結合藉由呼叫**SQLSetDescField**或**SQLSetDescRec**。 如需具名參數的詳細資訊，請參閱[依名稱 （具名參數） 的繫結參數](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)稍後在本章節中。 如需描述元的詳細資訊，請參閱[描述元](../../../odbc/reference/develop-app/descriptors.md)。  
  
 此章節包含下列主題。  
  
-   [繫結參數](../../../odbc/reference/develop-app/binding-parameters-odbc.md)  
  
-   [設定參數值](../../../odbc/reference/develop-app/setting-parameter-values.md)  
  
-   [傳送長資料](../../../odbc/reference/develop-app/sending-long-data.md)  
  
-   [SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)  
  
-   [程序參數](../../../odbc/reference/develop-app/procedure-parameters.md)  
  
-   [參數值陣列](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)
