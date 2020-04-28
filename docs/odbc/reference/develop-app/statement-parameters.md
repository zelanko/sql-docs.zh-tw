---
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
ms.openlocfilehash: 02327ff4bb6a1ac3ac57fbf7d3c6b09b70c11534
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306819"
---
# <a name="statement-parameters"></a>陳述式參數
*參數*是 SQL 語句中的變數。 例如，假設部分資料表具有名為 PartID、Description 和 Price 的資料行。 若要在不使用參數的情況下新增元件，則需要建立 SQL 語句，例如：  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 雖然此語句會插入新的訂單，但它不是正確的訂單輸入應用程式解決方案，因為插入的值無法在應用程式中硬式編碼。 另一個替代方式是使用要插入的值，在執行時間建立 SQL 語句。 這也不是很好的解決方案，因為在執行時間建立語句的複雜性。 最佳的解決方法是將**VALUES**子句的元素取代為問號（？）或*參數標記*：  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 然後會將參數標記繫結到應用程式變數。 若要加入新的資料列，應用程式只會設定變數的值，並執行語句。 然後驅動程式會擷取目前的變數值，再將其傳送給資料來源。 如果語句會多次執行，應用程式可以藉由準備語句來使進程更有效率。  
  
 剛剛顯示的語句可能會在訂單輸入應用程式中硬式編碼，以插入新的資料列。 不過，參數標記並不限於垂直應用程式。 針對任何應用程式，它們可以避免在執行時間建立 SQL 語句的困難，藉由避免文字來回轉換。 例如，剛剛顯示的元件識別碼最可能儲存在應用程式中做為整數。 如果未使用參數標記來建立 SQL 語句，則應用程式必須將元件識別碼轉換成文字，而且資料來源必須將它轉換回整數。 藉由使用參數標記，應用程式可以將元件識別碼當做整數傳送至驅動程式，這通常可以將它當做整數傳送至資料來源。 這會儲存兩個轉換。 對於 long 資料值而言，這非常重要，因為這類值的文字形式經常超過 SQL 語句的允許長度。  
  
 參數只有在 SQL 語句中的特定位置才有效。 例如，不允許在選取清單（ **select**語句所要傳回的資料行清單）中使用它們，也不允許同時做為二元運算子的兩個運算元（例如等號（=）），因為無法判斷參數類型。 一般而言，參數只在資料操作語言（DML）語句中有效，而不是在資料定義語言（DDL）語句中。 如需詳細資訊，請參閱附錄 C： SQL 文法中的[參數標記](../../../odbc/reference/appendixes/parameter-markers.md)。  
  
 當 SQL 語句叫用程式時，可以使用具名引數。 具名引數是由其名稱所識別，而不是其在 SQL 語句中的位置。 它們可以透過呼叫**SQLBindParameter**來系結，但參數是由 IPD （實參數描述項）的 SQL_DESC_NAME 欄位所識別，而非**SQLBindParameter**的*ParameterNumber*引數。 也可以藉由呼叫**SQLSetDescField**或**SQLSetDescRec**來系結。 如需具名引數的詳細資訊，請參閱本節稍後的[依名稱系結參數（具名引數）](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)。 如需描述項的詳細資訊，請參閱[描述](../../../odbc/reference/develop-app/descriptors.md)元。  
  
 此章節包含下列主題。  
  
-   [繫結參數](../../../odbc/reference/develop-app/binding-parameters-odbc.md)  
  
-   [設定參數值](../../../odbc/reference/develop-app/setting-parameter-values.md)  
  
-   [傳送長資料](../../../odbc/reference/develop-app/sending-long-data.md)  
  
-   [依 SQLGetData 抓取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)  
  
-   [程序參數](../../../odbc/reference/develop-app/procedure-parameters.md)  
  
-   [參數值陣列](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)
