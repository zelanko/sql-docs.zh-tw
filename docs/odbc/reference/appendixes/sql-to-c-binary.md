---
title: SQL 到 c： 二進位 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 16112ca3b66e0218efd54d3bf385e04cb654e3e4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622586"
---
# <a name="sql-to-c-binary"></a>SQL 到 C：二進位
二進位的 ODBC SQL 資料類型的識別項是：  
  
 SQL_BINARY  
  
 SQL_VARBINARY  
  
 SQL_LONGVARBINARY  
  
 下表顯示 ODBC C SQL 的二進位資料可能會轉換成的資料類型。 如需資料行和資料表中的詞彙說明，請參閱 <<c0> [ 轉換將資料從 SQL 到 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 類型識別碼|測試|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|（資料中的位元組長度）\* 2 < *Columnsize*<br /><br /> （資料中的位元組長度）\* 2 > = *Columnsize*|data<br /><br /> 截斷的資料|以位元組為單位的資料長度<br /><br /> 以位元組為單位的資料長度|n/a<br /><br /> 01004|  
|SQL_C_WCHAR|（字元長度的資料）\* 2 < *Columnsize*<br /><br /> （字元長度的資料）\* 2 > = *Columnsize*|data<br /><br /> 截斷的資料|以字元為單位的資料長度<br /><br /> 以字元為單位的資料長度|n/a<br /><br /> 01004|  
|SQL_C_BINARY|資料的位元組長度 < = *Columnsize*<br /><br /> 資料的位元組長度 > *Columnsize*|data<br /><br /> 截斷的資料|以位元組為單位的資料長度<br /><br /> 以位元組為單位的資料長度|n/a<br /><br /> 01004|  
  
 當 SQL 的二進位資料轉換成字元 C 資料時，來源資料的每個位元組 （8 位元） 被以兩個 ASCII 字元。 這些字元是十六進位格式的數字的 ASCII 字元表示。 例如，二進位 00000001 會轉換成"01"，而二進位 11111111 會轉換成"FF"。  
  
 驅動程式一律會將個別的位元組轉換成十六進位數字組，並終止 null 位元組字元字串。 因為這個緣故，如果*Columnsize*是偶數，且小於已轉換資料，也就是最後一個位元組的長度 **TargetValuePtr*不使用緩衝區。 （已轉換的資料需要偶數數目的位元組、 下一步 倒數第二個位元組是 null 位元組，而且不能使用的最後一個位元組）。  
  
> [!NOTE]  
>  應用程式開發人員都不要字元 C 資料類型的二進位 SQL 將資料繫結項目。 此轉換通常是緩慢又沒有效率。
