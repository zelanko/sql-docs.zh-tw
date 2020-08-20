---
description: 小數位數
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0c56d0d4cdd4c40c2174085d80618bbcc58af14e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456615"
---
# <a name="decimal-digits"></a>小數位數
十進位和數值資料類型的 *小* 數位數定義為小數點右邊的最大位數，或資料的小數位數。 對於近似的浮點數資料行或參數，小數位數是未定義的，因為小數點右邊的位數不是固定的。 若為包含秒陣列件的日期時間或間隔資料，小數位數會定義為數據的秒陣列件中小數點右邊的位數。  
  
 針對 SQL_DECIMAL 和 SQL_NUMERIC 資料類型，最大的小數位數通常與最大精確度相同。 不過，某些資料來源會對最大刻度強加不同的限制。 為了判斷資料類型所允許的最小和最大刻度，應用程式會呼叫 **SQLGetTypeInfo**。  
  
 下表顯示為每個簡潔的 SQL 資料類型定義的小數位數。  
  
|SQL 類型|十進位數字|  
|--------------|--------------------|  
|所有字元和二進位類型 [a]|n/a|  
|SQL_DECIMAL<br />SQL_NUMERIC|小數點右邊的已定義數位數目。 例如，定義為數值 (10，3) 的資料行小數位數為3。 這可以是負數，以支援不使用指數標記法的大量數位儲存;例如，"12000" 可能會以-3 的小數位數儲存為 "12"。|  
|除了 SQL_DECIMAL 和 SQL_NUMERIC [a] 以外的所有精確數數值型別|0|  
|所有近似的資料類型 [a]|n/a|  
|SQL_TYPE_DATE，以及所有不含秒陣列件的間隔類型 [a]|n/a|  
|除了 SQL_TYPE_DATE 以外的所有日期時間類型，以及所有具有秒陣列件的間隔類型|值的秒數部分中小數點右邊的位數， (小數秒) 。 此數位不能為負數。|  
|SQL_GUID|n/a|  
  
 [a] 此資料類型會忽略**SQLBindParameter**的*DecimalDigits*引數。  
  
 針對小數位數傳回的值不會對應至任何一個描述項欄位中的值。 根據資料類型而定，這些值可以來自 SQL_DESC_SCALE 或 SQL_DESC_PRECISION 欄位，如下表所示。  
  
|SQL 類型|對應的描述項欄位<br /><br /> 十進位數|  
|--------------|----------------------------------------------------------|  
|所有字元和二進位類型|n/a|  
|所有精確的數數值型別|SCALE|  
|SQL_BIT|n/a|  
|所有近似的數數值型別|n/a|  
|所有日期時間類型|PRECISION|  
|具有秒陣列件的所有間隔類型|PRECISION|  
|所有不含秒陣列件的間隔類型|n/a|
