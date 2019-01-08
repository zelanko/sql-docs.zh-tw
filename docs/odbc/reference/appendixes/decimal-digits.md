---
title: 十進位數字 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: f7b9a69941364b32e6b43d79f2d092511fd61f22
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52506078"
---
# <a name="decimal-digits"></a>小數位數
*十進位數字*的 decimal 與 numeric 資料類型會定義為小數點右邊或資料的小數位數的數字的數目上限。 近似浮點數的數字資料行或參數，因為不固定的小數點右邊的位數，未定義小數位數。 包含秒元件的日期時間或間隔的資料，小數位數被指資料的秒數元件之小數點右邊的位數。  
  
 SQL_DECIMAL 和 SQL_NUMERIC 資料類型最大小數位數通常是最大有效位數相同。 不過，某些資料來源會造成最大的標尺上的個別限制。 若要判斷資料類型所允許的最小和最大縮放比例，應用程式會呼叫**SQLGetTypeInfo**。  
  
 下表顯示針對每種精簡的 SQL 資料類型所定義的十進位數字。  
  
|SQL 類型|十進位數字|  
|--------------|--------------------|  
|所有的字元和二進位類型 [a]|n/a|  
|SQL_DECIMAL<br />SQL_NUMERIC|定義的小數點右邊的數字數目。 例如，定義為 NUMERIC(10,3) 資料行的小數位數為 3。 這可以是負數以支援非常大量的儲存體，而不需使用指數標記法;比方說，無法儲存"12000"為"12"數位數為-3。|  
|SQL_DECIMAL 和 SQL_NUMERIC [a] 以外的所有精確數值類型|0|  
|所有近似資料類型 [a]|n/a|  
|SQL_TYPE_DATE，以及所有的間隔類型，與任何秒數元件 [a]|n/a|  
|SQL_TYPE_DATE，以外的所有日期時間類型和其秒元件的所有間隔類型|中的值 （毫秒） 的秒數部分在小數點右邊位數數目。 此數目不可為負數。|  
|SQL_GUID|n/a|  
  
 [a] *DecimalDigits*引數**SQLBindParameter**會忽略此資料型別。  
  
 傳回十進位數字的值不符中任何一個的描述項欄位的值。 值可以來自 SQL_DESC_SCALE 或 SQL_DESC_PRECISION 欄位中的，根據資料類型下, 表所示。  
  
|SQL 類型|對應到描述項欄位<br /><br /> 十進位數字|  
|--------------|----------------------------------------------------------|  
|所有的字元和二進位類型|n/a|  
|所有的精確數值類型|SCALE|  
|SQL_BIT|n/a|  
|所有的近似數值類型|n/a|  
|所有日期時間類型|PRECISION|  
|所有的間隔類型以秒數元件|PRECISION|  
|使用沒有秒元件的所有間隔類型|n/a|
