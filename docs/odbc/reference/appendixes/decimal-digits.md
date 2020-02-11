---
title: 十進位數 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- size of data types [ODBC]
- decimal digits of data types [ODBC]
- data types [ODBC], decimal digits
- SQL data types [ODBC], column characteristics
ms.assetid: 07f3d1fc-b4ee-4693-b342-330b2231b6d0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6e58551ae3c6edda3cd865817223fd8052d03ec5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68130047"
---
# <a name="decimal-digits"></a>小數位數
Decimal 和 numeric 資料類型的*十進位*數定義為小數點右邊的最大位數，或資料的刻度。 對於近似的浮點數資料行或參數，小數位數是未定義的，因為小數點右邊的位數不是固定的。 對於包含秒陣列件的 datetime 或 interval 資料，小數位數會定義為數據的秒陣列件中小數點右邊的位數。  
  
 對於 SQL_DECIMAL 和 SQL_NUMERIC 資料類型，最大的小數位數通常與最大精確度相同。 不過，某些資料來源會對最大規模施加不同的限制。 若要判斷資料類型所允許的最小和最大刻度，應用程式會呼叫**SQLGetTypeInfo**。  
  
 下表顯示每個簡潔 SQL 資料類型所定義的十進位數。  
  
|SQL 類型|十進位數字|  
|--------------|--------------------|  
|所有字元和二進位類型 [a]|n/a|  
|SQL_DECIMAL<br />SQL_NUMERIC|小數點右邊定義的位數。 例如，定義為 NUMERIC （10，3）之資料行的小數位數為3。 這可以是負數，而不需要使用指數標記法來支援非常大的數位儲存;例如，"12000" 可以儲存為 "12"，且小數值為-3。|  
|SQL_DECIMAL 和 SQL_NUMERIC 以外的所有精確數數值型別 [a]|0|  
|所有近似資料類型 [a]|n/a|  
|SQL_TYPE_DATE 和所有間隔類型，但不含秒陣列件 [a]|n/a|  
|除了 SQL_TYPE_DATE 以外的所有 datetime 類型，以及具有秒陣列件的所有間隔類型|在值的秒數部分中，小數點右邊的位數（小數秒）。 這個數位不可以是負數。|  
|SQL_GUID|n/a|  
  
 [a] 這個資料類型會忽略**SQLBindParameter**的*DecimalDigits*引數。  
  
 針對十進位數傳回的值不會對應到任何一個描述項欄位中的值。 值可以來自 SQL_DESC_SCALE 或 SQL_DESC_PRECISION 欄位，視資料類型而定，如下表所示。  
  
|SQL 類型|對應至的描述項欄位<br /><br /> 十進位數|  
|--------------|----------------------------------------------------------|  
|所有字元和二進位類型|n/a|  
|所有精確的數數值型別|SCALE|  
|SQL_BIT|n/a|  
|所有近似數數值型別|n/a|  
|所有日期時間類型|PRECISION|  
|包含秒陣列件的所有間隔類型|PRECISION|  
|沒有秒陣列件的所有間隔類型|n/a|
