---
title: SQL 到 c： 二進位 |Microsoft 文件
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
ms.topic: article
helpviewer_keywords:
- converting data from SQL to c types [ODBC], binary
- binary data type [ODBC]
- data conversions from SQL to C types [ODBC], binary
- binary data transfers [ODBC]
ms.assetid: 8c519072-ae4c-4d32-9d4e-775e3d3d6389
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 36f1faed079da9dd8b3d04f659bc079583abd044
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sql-to-c-binary"></a>SQL 到 c： 二進位
二進位的 ODBC SQL 資料類型的識別項是：  
  
 SQL_BINARY  
  
 SQL_VARBINARY  
  
 SQL_LONGVARBINARY  
  
 下表顯示 ODBC C 資料類型可能會轉換 SQL 的二進位資料。 如需的資料行和資料表中的詞彙說明，請參閱[轉換資料從 SQL 到 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 類型識別碼|測試|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|（位元組長度的資料）\* 2 < *Columnsize*<br /><br /> （位元組長度的資料）\* 2 > = *Columnsize*|資料<br /><br /> 截斷的資料|以位元組為單位的資料長度<br /><br /> 以位元組為單位的資料長度|n/a<br /><br /> 01004|  
|SQL_C_WCHAR|（字元長度的資料）\* 2 < *Columnsize*<br /><br /> （字元長度的資料）\* 2 > = *Columnsize*|資料<br /><br /> 截斷的資料|以字元為單位的資料長度<br /><br /> 以字元為單位的資料長度|n/a<br /><br /> 01004|  
|SQL_C_BINARY|資料的位元組長度 < = *Columnsize*<br /><br /> 資料的位元組長度 > *Columnsize*|資料<br /><br /> 截斷的資料|以位元組為單位的資料長度<br /><br /> 以位元組為單位的資料長度|n/a<br /><br /> 01004|  
  
 當二進位 SQL 資料轉換成 C 字元資料時，來源資料的每個位元組 （8 位元） 被以兩個 ASCII 字元。 這些字元出現在其十六進位格式的數字的 ASCII 字元表示法。 例如，二進位 00000001 會轉換為"01"，而二進位 11111111 會轉換成"FF"。  
  
 驅動程式一律會將個別的位元組轉換為十六進位數字組，並終止 null 位元組的字元字串。 因為這個緣故，如果*Columnsize*甚至也未轉換的資料，最後一個位元組的長度小於 **TargetValuePtr*不會使用緩衝區。 （轉換的資料需要偶數個位元組下, 一個到最後一個位元組是 null 的位元組，而且不能使用的最後一個位元組。）  
  
> [!NOTE]  
>  應用程式開發人員都建議您不要從二進位 SQL 資料繫結至字元 C 資料類型。 此轉換通常是緩慢又沒有效率。
