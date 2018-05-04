---
title: 十進位數字 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- size of data types [ODBC]
- decimal digits of data types [ODBC]
- data types [ODBC], decimal digits
- SQL data types [ODBC], column characteristics
ms.assetid: 07f3d1fc-b4ee-4693-b342-330b2231b6d0
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3b4aaf614ac165d7ca867b3bf394ea942a992e19
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="decimal-digits"></a>十進位數字
*十進位數字*的 decimal 和 numeric 資料型別定義為小數點右邊的，或資料的小數位數的數字的數目上限。 近似浮點數的數字資料行或參數，因為不固定的小數點右邊的位數，未定義小數位數。 包含秒數元件的日期時間或間隔的資料，對於十進位數字定義為資料的秒數元件中的小數點右邊的位數。  
  
 SQL_DECIMAL 和 SQL_NUMERIC 資料類型最大小數位數通常是最大有效位數相同。 不過，某些資料來源限制個別最大小數位數。 若要判斷資料類型所允許的最小和最大比例，應用程式呼叫**SQLGetTypeInfo**。  
  
 下表顯示每個簡潔的 SQL 資料類型所定義的十進位數字。  
  
|SQL 類型|十進位數字|  
|--------------|--------------------|  
|所有的字元和二進位類型 [a]|n/a|  
|SQL_DECIMAL<br />SQL_NUMERIC|定義的小數點右邊位數的數目。 例如，定義為 NUMERIC(10,3) 資料行的小數位數為 3。 這可以是負數，而不使用指數標記法; 支援非常大量的儲存體例如，"12000 「 無法儲存為"12"小數位數為 – 3。|  
|SQL_DECIMAL 和 SQL_NUMERIC [a] 以外的所有精確數值類型|0|  
|所有近似資料類型 [a]|n/a|  
|SQL_TYPE_DATE，以及與任何秒數元件 [a] 的所有間隔類型|n/a|  
|SQL_TYPE_DATE，以外的所有日期時間類型和秒元件的所有間隔類型|中的值 （小數秒數） 的秒鐘部分在小數點右邊位數數目。 這個數字不能為負數。|  
|SQL_GUID|n/a|  
  
 [a] *d*引數的**SQLBindParameter**會忽略此資料類型。  
  
 傳回十進位數字的值中任何一個描述元欄位的值不符。 值可以來自 SQL_DESC_SCALE 或 SQL_DESC_PRECISION 欄位中的，根據資料類型下, 表所示。  
  
|SQL 類型|對應至描述項欄位<br /><br /> 十進位數字|  
|--------------|----------------------------------------------------------|  
|所有的字元和二進位的型別|n/a|  
|所有的精確數值類型|SCALE|  
|SQL_BIT|n/a|  
|所有的近似數值類型|n/a|  
|所有的日期時間類型|PRECISION|  
|所有的間隔類型，以秒數元件|PRECISION|  
|所有的間隔類型，具有沒有秒數元件|n/a|
