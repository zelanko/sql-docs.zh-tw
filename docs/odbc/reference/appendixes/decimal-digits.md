---
title: 十進位數字 |微軟文件
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
ms.openlocfilehash: 4921a6162b6d711e657f223b5be5783dfa37bca8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285158"
---
# <a name="decimal-digits"></a>小數位數
十進位和數位資料類型*的小數位數*定義為小數點右側的最大位數或數據的比例。 對於近似的浮點數列或參數,比例未定義,因為小數點右側的數字數不是固定的。 對於包含秒分量的日期時間或間隔數據,十進位數字定義為數據秒元件中小數點右側的數字數。  
  
 對於SQL_DECIMAL和SQL_NUMERIC數據類型,最大比例通常與最大精度相同。 但是,某些數據源對最大比例施加了單獨的限制。 要確定資料類型允許的最小和最大比例,應用程式呼叫**SQLGetTypeInfo**。  
  
 為每種簡潔的 SQL 數據類型定義的小數位數顯示在下表中。  
  
|SQL 類型|十進位數字|  
|--------------|--------------------|  
|所有字元和二進位類型[a]|n/a|  
|SQL_DECIMAL<br />SQL_NUMERIC|小數點右側的已定義數字數。 例如,定義為數位(10,3)的列比例為 3。 這可以是負數,以支援存儲非常大的數位,而無需使用指數表示法;例如,"12000"可以存儲為"12",其比例為-3。|  
|SQL_DECIMAL與SQL_NUMERIC以外的所有精確數值類型|0|  
|所有近似資料類型[a]|n/a|  
|SQL_TYPE_DATE,並且所有間隔類型,沒有秒分量 [a]|n/a|  
|除SQL_TYPE_DATE之外的所有日期時間類型以及具有秒元件的所有間隔類型|值的秒部分(分數秒)中小數點右側的數字數。 此數位不能為負數。|  
|SQL_GUID|n/a|  
  
 [a] 此資料型態會忽略**SQLBind 參數**的*十進位參數*。  
  
 為小數位數返回的值與任何一個描述符欄位中的值不對應。 這些值可以來自SQL_DESC_SCALE或SQL_DESC_PRECISION欄位,具體取決於數據類型,如下表所示。  
  
|SQL 類型|與<br /><br /> 十進位數字|  
|--------------|----------------------------------------------------------|  
|所有字元與二進位型態|n/a|  
|所有不確切的數值類型|SCALE|  
|SQL_BIT|n/a|  
|所有近似數值類型|n/a|  
|所有日期時間類型|PRECISION|  
|具有秒元件的所有間隔型態|PRECISION|  
|所有間隔型態,無秒分量|n/a|
