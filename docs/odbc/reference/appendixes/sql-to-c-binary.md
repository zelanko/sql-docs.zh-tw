---
title: SQL 到 C： Binary |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e280afb03eeac46a58943d276137e2019340a0a2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68057005"
---
# <a name="sql-to-c-binary"></a>SQL 到 C：二進位
二進位 ODBC SQL 資料類型的識別碼為：  
  
 SQL_BINARY  
  
 SQL_VARBINARY  
  
 SQL_LONGVARBINARY  
  
 下表顯示二進位 SQL 資料可能轉換成的 ODBC C 資料類型。 如需資料表中的資料行和詞彙的說明，請參閱將[資料從 SQL 轉換成 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 類型識別碼|測試|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|（資料的位元組長度）\* 2 < *BufferLength*<br /><br /> （資料的位元組長度）\* 2 >= *BufferLength*|資料<br /><br /> 截斷的資料|資料長度（以位元組為單位）<br /><br /> 資料長度（以位元組為單位）|n/a<br /><br /> 01004|  
|SQL_C_WCHAR|（資料的字元長度）\* 2 < *BufferLength*<br /><br /> （資料的字元長度）\* 2 >= *BufferLength*|資料<br /><br /> 截斷的資料|資料長度（以字元為單位）<br /><br /> 資料長度（以字元為單位）|n/a<br /><br /> 01004|  
|SQL_C_BINARY|資料 <的位元組長度 = *BufferLength*<br /><br /> 資料 > *BufferLength*的位元組長度|資料<br /><br /> 截斷的資料|資料長度（以位元組為單位）<br /><br /> 資料長度（以位元組為單位）|n/a<br /><br /> 01004|  
  
 當二進位 SQL 資料轉換成字元 C 資料時，來源資料的每個位元組（8位）都會以兩個 ASCII 字元來表示。 這些字元是十六進位格式之數位的 ASCII 字元標記法。 例如，二進位00000001會轉換成 "01"，而二進位11111111會轉換成 "FF"。  
  
 驅動程式一律會將個別位元組轉換成成對的十六進位數位，並以 null 位元組結束字元字串。 因此，如果*BufferLength*是偶數且小於已轉換資料的長度，則不會使用 **TargetValuePtr*緩衝區的最後一個位元組。 （已轉換的資料需要偶數個位元組，下一個到最後一個位元組是 null 位元組，而且無法使用最後一個位元組）。  
  
> [!NOTE]  
>  不鼓勵應用程式開發人員將二進位 SQL 資料系結至字元 C 資料類型。 這種轉換通常沒有效率，而且速度變慢。
