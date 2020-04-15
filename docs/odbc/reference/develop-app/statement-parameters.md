---
title: 語句參數 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 02327ff4bb6a1ac3ac57fbf7d3c6b09b70c11534
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306819"
---
# <a name="statement-parameters"></a>陳述式參數
*參數*是 SQL 語句中的變數。 例如,假設「零件」表具有名為「PartID」、「說明」和「價格」的列。 要添加沒有參數的零件,需要建構 SQL 語句,例如:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 儘管此語句插入了新訂單,但它不是訂單輸入應用程式的良好解決方案,因為要插入的值在應用程式中不能硬編碼。 另一種方法是在運行時使用要插入的值構造 SQL 語句。 由於在運行時構造語句的複雜性,這還不是很好的解決方案。 最佳解決方案是用問號 (?) 或*參數標記*取代**VALUE**子句的元素:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 然後會將參數標記繫結到應用程式變數。 要添加新行,應用程式只需設置變數的值並執行語句。 然後驅動程式會擷取目前的變數值，再將其傳送給資料來源。 如果語句將執行多次,則應用程式可以通過準備語句使該過程更加高效。  
  
 剛剛顯示的語句可能是在訂單輸入應用程式中硬編碼的,用於插入新行。 但是,參數標記並不限於垂直應用。 對於任何應用程式,它們通過避免與文本轉換來簡化在運行時建構 SQL 語句的難度。 例如,剛才顯示的部件 ID 最有可能作為整數存儲在應用程式中。 如果 SQL 語句建構時沒有參數標記,則應用程式必須將部件 ID 轉換為文本,數據源必須將其轉換回整數。 通過使用參數標記,應用程式可以將部件 ID 作為整數發送到驅動程式,該整數通常可以將其作為整數發送到數據源。 這樣可以節省兩次轉換。 對於長數據值,這一點非常重要,因為此類值的文本形式經常超過 SQL 語句的允許長度。  
  
 參數僅在 SQL 語句中的某些位置有效。 例如,它們不允許在選擇清單中(**由 SELECT**語句返回的列清單),也不允許它們作為二進制運算符(如等號 (*)的兩個操作數,因為無法確定參數類型。 通常,參數僅在數據操作語言 (DML) 語句中有效,而在數據定義語言 (DDL) 語句中無效。 有關詳細資訊,請參閱附錄 C 中的[參數標記](../../../odbc/reference/appendixes/parameter-markers.md):SQL 語法。  
  
 當 SQL 語句調用過程時,可以使用命名參數。 命名參數由名稱識別,而不是由它們在 SQL 語句中的位置標識。 它們可以由對**SQLBind 參數**的呼叫綁定,但參數由 IPD 的SQL_DESC_NAME欄位(實現參數描述符)標識,而不是由**SQLBind 參數**的*參數編號*參數標識。 它們也可以通過調用**SQLSetDescField**或**SQLSetDescRec**來綁定。 有關命名參數的詳細資訊,請參閱本節後面的[「按名稱(命名參數)綁定參數](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)」。。 有關描述符的詳細資訊,請參閱[描述子](../../../odbc/reference/develop-app/descriptors.md)。  
  
 此章節包含下列主題。  
  
-   [繫結參數](../../../odbc/reference/develop-app/binding-parameters-odbc.md)  
  
-   [設定參數值](../../../odbc/reference/develop-app/setting-parameter-values.md)  
  
-   [傳送長資料](../../../odbc/reference/develop-app/sending-long-data.md)  
  
-   [依 SQLGetData 偵測參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)  
  
-   [程序參數](../../../odbc/reference/develop-app/procedure-parameters.md)  
  
-   [參數值陣列](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)
