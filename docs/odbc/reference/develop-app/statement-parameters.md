---
title: 陳述式參數 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- statement parameters [ODBC]
ms.assetid: 58d5b166-2578-4699-a560-1f1e6d86c49a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b366ddd7a665112e6b40b814b13037a517d623a5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149356"
---
# <a name="statement-parameters"></a>陳述式參數
A*參數*是 SQL 陳述式中的變數。 例如，假設組件資料表包含名為 PartID、 描述和價格的資料行。 若要加入的組件不含參數需要建構 SQL 陳述式，例如：  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 雖然這個陳述式會插入新的順序，不適合訂單輸入應用程式的絕佳解決方案因為插入的值不能是硬式編碼應用程式中。 替代方式是建構 SQL 陳述式在執行階段，使用要插入的值。 這也是不好的解決方案，因為在執行階段建構陳述式的複雜度。 最好的解決方案是要取代的項目**值**子句以問號 （？），或*參數標記*:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 然後會將參數標記繫結到應用程式變數。 若要加入新的資料列，應用程式必須僅設定變數的值，並執行陳述式。 然後驅動程式會擷取目前的變數值，再將其傳送給資料來源。 如果陳述式將會執行多次，應用程式可讓處理程序更有效率預備此陳述式。  
  
 如上所示的陳述式可能是硬式編碼在訂單項目應用程式中插入新的資料列。 不過，不一定要垂直應用程式，參數標記。 針對任何應用程式，其可簡化在執行階段建構 SQL 陳述式，藉由避免轉換文字的困難度。 比方說，剛才顯示的部分識別碼是最有可能儲存在應用程式中做為整數。 如果 SQL 陳述式會建構不含參數標記，應用程式必須轉換成文字的部分識別碼和資料來源必須將它轉換回整數。 藉由使用參數標記，應用程式可以部分識別碼傳送至驅動程式通常可以將它傳送至資料來源做為整數的整數。 這會儲存兩種轉換。 Long 資料值，這是很重要，因為這類值的文字形式經常會超過 SQL 陳述式的允許的長度。  
  
 參數只能在 SQL 陳述式中的特定位置中都有效。 比方說，它們不被允許的選取清單中 (要傳回之資料行清單**選取**陳述式)，也不他們允許等號 （=），這類的二元運算子的兩個運算元為因為它是不可能判斷參數類型。 一般而言，參數會只在資料操作語言 (DML) 陳述式，而不是在資料定義語言 (DDL) 陳述式時才有效。 如需詳細資訊，請參閱 <<c0> [ 參數標記](../../../odbc/reference/appendixes/parameter-markers.md)附錄 c:SQL 文法。  
  
 可以使用 SQL 陳述式時叫用的程序中，然後再具名參數。 具名的參數是以其名稱識別，不是由在 SQL 陳述式中的位置。 藉由呼叫繫結**SQLBindParameter**，但參數不是識別 ipd （實作參數描述項，） 與 SQL_DESC_NAME 欄位*Sqlbindparameter*引數**SQLBindParameter**。 也可以結合藉由呼叫**SQLSetDescField**或是**SQLSetDescRec**。 如需有關具名參數的詳細資訊，請參閱[依名稱 （具名參數） 的繫結參數](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)稍後這一節。 如需描述項的詳細資訊，請參閱[描述元](../../../odbc/reference/develop-app/descriptors.md)。  
  
 此章節包含下列主題。  
  
-   [繫結參數](../../../odbc/reference/develop-app/binding-parameters-odbc.md)  
  
-   [設定參數值](../../../odbc/reference/develop-app/setting-parameter-values.md)  
  
-   [傳送長資料](../../../odbc/reference/develop-app/sending-long-data.md)  
  
-   [SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)  
  
-   [程序參數](../../../odbc/reference/develop-app/procedure-parameters.md)  
  
-   [參數值陣列](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)
