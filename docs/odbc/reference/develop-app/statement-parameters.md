---
description: 陳述式參數
title: 語句參數 |Microsoft Docs
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
ms.openlocfilehash: 7400367d4b237d2d0e22c6363d1559eb89506d7d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482891"
---
# <a name="statement-parameters"></a>陳述式參數
*參數*是 SQL 語句中的變數。 例如，假設部分資料表具有名為 PartID、Description 和 Price 的資料行。 若要加入不含參數的元件，則需要建立 SQL 語句，例如：  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 雖然此語句會插入新的訂單，但這對訂單輸入應用程式而言並不是很好的解決方案，因為插入的值無法在應用程式中硬式編碼。 替代方法是在執行時間使用要插入的值來建立 SQL 語句。 這也不是很好的解決方案，因為它會在執行時間建立語句的複雜度。 最好的解決方法是將 **VALUES** 子句的元素取代為問號 (？ ) 或 *參數標記*：  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 然後會將參數標記繫結到應用程式變數。 若要加入新的資料列，應用程式只會設定變數的值，並執行語句。 然後驅動程式會擷取目前的變數值，再將其傳送給資料來源。 如果語句會執行多次，應用程式可以藉由準備語句來讓進程更有效率。  
  
 剛剛顯示的語句可能會在訂單輸入應用程式中硬式編碼，以插入新的資料列。 不過，參數標記不限於垂直應用程式。 針對任何應用程式，它們可以避免在執行時間建立 SQL 語句的困難，方法是避免來回轉換文字。 例如，只顯示的元件識別碼最可能會以整數形式儲存在應用程式中。 如果不使用參數標記來建立 SQL 語句，則應用程式必須將部分識別碼轉換為文字，且資料來源必須將它轉換回整數。 藉由使用參數標記，應用程式可以將元件識別碼以整數形式傳送至驅動程式，通常可以將它以整數的形式傳送到資料來源。 這會節省兩個轉換。 若為 long 資料值，這非常重要，因為這類值的文字形式通常會超過 SQL 語句的允許長度。  
  
 參數只在 SQL 語句中的特定位置有效。 例如，在選取清單中不允許它們， (**select** 語句所要傳回的資料行清單) ，也不能同時做為二元運算子的兩個運算元，例如等號 (=) ，因為這可能無法判斷參數類型。 一般而言，參數只在資料操作語言中有效， (DML) 語句，而不是在資料定義語言 (DDL) 語句中。 如需詳細資訊，請參閱附錄 C： SQL 文法中的 [參數標記](../../../odbc/reference/appendixes/parameter-markers.md) 。  
  
 當 SQL 語句叫用程式時，可以使用具名引數。 具名引數是由其名稱來識別，而不是依其在 SQL 語句中的位置來識別。 您可以透過呼叫**SQLBindParameter**來系結，但參數是由 IPD (實參數描述項) 的 SQL_DESC_NAME 欄位所識別，而不是由**SQLBindParameter**的*ParameterNumber*引數所識別。 它們也可以藉由呼叫 **SQLSetDescField** 或 **SQLSetDescRec**來系結。 如需有關具名引數的詳細資訊，請參閱本節稍後的 [ (具名引數的名稱系結參數) ](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)。 如需描述項的詳細資訊，請參閱 [描述](../../../odbc/reference/develop-app/descriptors.md)項。  
  
 此章節包含下列主題。  
  
-   [繫結參數](../../../odbc/reference/develop-app/binding-parameters-odbc.md)  
  
-   [設定參數值](../../../odbc/reference/develop-app/setting-parameter-values.md)  
  
-   [傳送長資料](../../../odbc/reference/develop-app/sending-long-data.md)  
  
-   [依 SQLGetData 抓取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)  
  
-   [程序參數](../../../odbc/reference/develop-app/procedure-parameters.md)  
  
-   [參數值陣列](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)
