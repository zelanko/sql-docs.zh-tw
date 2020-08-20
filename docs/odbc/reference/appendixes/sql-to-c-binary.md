---
description: SQL 到 C：二進位
title: SQL 到 C：二進位 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to c types [ODBC], binary
- binary data type [ODBC]
- data conversions from SQL to C types [ODBC], binary
- binary data transfers [ODBC]
ms.assetid: 8c519072-ae4c-4d32-9d4e-775e3d3d6389
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 229611308c2dba83a8d793810eb5a5443cbd7062
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456551"
---
# <a name="sql-to-c-binary"></a>SQL 到 C：二進位
二進位 ODBC SQL 資料類型的識別碼如下：  
  
 SQL_BINARY  
  
 SQL_VARBINARY  
  
 SQL_LONGVARBINARY  
  
 下表顯示二進位 SQL 資料可能轉換成的 ODBC C 資料類型。 如需資料表中的資料行和詞彙的說明，請參閱將 [資料從 SQL 轉換成 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 類型識別碼|測試|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR| (位元組長度的資料) \* 2 < *BufferLength*<br /><br />  (位元組長度的資料) \* 2 >= *BufferLength*|資料<br /><br /> 截斷的資料|資料的長度（以位元組為單位）<br /><br /> 資料的長度（以位元組為單位）|n/a<br /><br /> 01004|  
|SQL_C_WCHAR| (字元長度的資料) \* 2 < *BufferLength*<br /><br />  (字元長度的資料) \* 2 >= *BufferLength*|資料<br /><br /> 截斷的資料|資料的長度（以字元為單位）<br /><br /> 資料的長度（以字元為單位）|n/a<br /><br /> 01004|  
|SQL_C_BINARY|資料 <的位元組長度 = *BufferLength*<br /><br /> 資料 > *BufferLength*的位元組長度|資料<br /><br /> 截斷的資料|資料的長度（以位元組為單位）<br /><br /> 資料的長度（以位元組為單位）|n/a<br /><br /> 01004|  
  
 當二進位 SQL 資料轉換成字元 C 資料時，每個位元組 (8 位的來源資料) 都會以兩個 ASCII 字元表示。 這些字元是十六進位格式之數位的 ASCII 字元標記法。 例如，二進位00000001會轉換成 "01"，而二進位11111111會轉換成 "FF"。  
  
 驅動程式一律會將個別位元組轉換成成對的十六進位數位，並以 null 位元組結束字元字串。 因此，如果 *BufferLength* 為偶數，而且小於轉換資料的長度，則不會使用 **TargetValuePtr* 緩衝區的最後一個位元組。  (轉換的資料需要偶數位節數目，下一個到最後一個位元組是 null 位元組，而且無法使用最後一個位元組。 )   
  
> [!NOTE]  
>  不建議應用程式開發人員將二進位 SQL 資料系結至字元 C 資料類型。 這項轉換通常沒有效率且速度很慢。
