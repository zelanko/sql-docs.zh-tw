---
title: "Microsoft Excel 的資料型別 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], Excel driver
- Excel data types [ODBC]
- Jet-based ODBC drivers [ODBC], Excel driver
- desktop database drivers [ODBC], Excel driver
- ODBC desktop database drivers [ODBC], Excel driver
- Excel driver [ODBC], data types
ms.assetid: 7b44c8e5-0bc3-4912-8a5d-56f4d5562fe6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eeb2bc72ce34141eb3dbdca3f952dca0c476c2dd
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="microsoft-excel-data-types"></a>Microsoft Excel 資料類型
下表顯示如何將 Microsoft Excel 驅動程式資料類型對應至 ODBC SQL 資料類型。 Microsoft Excel 驅動程式會將這些資料類型指派給資料行中的資料為基礎的 Microsoft Excel 資料表中資料行。  
  
|Microsoft Excel 資料類型|ODBC 資料類型|  
|-------------------------------|--------------------|  
|CURRENCY|SQL_NUMERIC|  
|DATETIME|SQL_TIMESTAMP|  
|邏輯|SQL_BIT|  
|NUMBER|SQL_DOUBLE|  
|TEXT|SQL_VARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo**傳回 ODBC SQL 資料類型。 所有的轉換中的 < 附錄 D *ODBC 程式設計人員參考*支援本主題稍早所列的 ODBC SQL 資料類型。  
  
 下表顯示 Microsoft Excel 資料類型的限制。  
  
|資料類型|Description|  
|---------------|-----------------|  
|加密的資料|Microsoft Excel 驅動程式無法讀取加密的資料。|  
|錯誤字串|Microsoft Excel 驅動程式不能傳回 Microsoft Excel 錯誤值的字元字串 (# n/A ！，#VALUE ！，#REF ！、 #DIV/0 ！，#NUM ！，#NAME？，和 #NULL ！)，但改為傳回 NULL。|  
|邏輯|SQL_C_CHAR 緩衝區中傳回的邏輯資料行中的值為 0 或 1。|  
|NUMBER|如果建立整數資料行時，您可以輸入太大的整數資料類型的數字，並才能插入資料包含非整數值，以資料行可能會轉換成 SQL_DOUBLE 結果。|  
|TEXT|當資料行的資料列包含一個以上的 Microsoft Excel 資料類型時，ODBC Microsoft Excel 驅動程式會指派給資料行的 SQL_VARCHAR 資料類型。 沒有一個例外狀況： 如果資料行包含只有兩個或三個日期時間資料型別 （日期、 時間和日期時間），ODBC Microsoft Excel 驅動程式會將 SQL_TIMESTAMP 資料類型指派給資料行。<br /><br /> 建立文字資料行的零或未指定的長度實際上會傳回 255 個位元組的資料行。<br /><br /> 字元字串常值可以包含任何的 ANSI 字元 （1-255 個十進位）。 您可以使用兩個連續單引號 （'） 來表示一個單引號 （'）。<br /><br /> SQL_VARCHAR 資料類型，將插入的資料行的 null 值會變更為 SQL_VARCHAR 資料行的資料類型。|  
  
 資料類型的多個限制可以在[資料型別限制](../../odbc/microsoft/data-type-limitations.md)。

