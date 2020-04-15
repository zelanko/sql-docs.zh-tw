---
title: 'SQL 到 C: 二進位 |微軟文件'
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
ms.openlocfilehash: 70b0ce72f650e61b83ec99b0727752612d18da52
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298819"
---
# <a name="sql-to-c-binary"></a>SQL 到 C：二進位
二進位 ODBC SQL 資料類型的識別碼包括:  
  
 SQL_BINARY  
  
 SQL_VARBINARY  
  
 SQL_LONGVARBINARY  
  
 下表顯示了可轉換為二進位 SQL 資料的 ODBC C 資料類型。 有關表中列與字語的說明,請參考[資料從 SQL 轉換為 C 資料型態](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
|C 類型識別碼|測試|**目標價值Ptr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|(資料位元組長度)\* 2 <*緩衝區長度*<br /><br /> (資料位元組長度)\* 2 >=*緩衝區長度*|資料<br /><br /> 截斷的資料|以位元組為單位的資料長度<br /><br /> 以位元組為單位的資料長度|n/a<br /><br /> 01004|  
|SQL_C_WCHAR|(資料字元長度)\* 2 <*緩衝區長度*<br /><br /> (資料字元長度)\* 2 >=*緩衝區長度*|資料<br /><br /> 截斷的資料|字元中的資料長度<br /><br /> 字元中的資料長度|n/a<br /><br /> 01004|  
|SQL_C_BINARY|資料<位元組長度 =*緩衝區長度*<br /><br /> >*緩衝區長度*的資料位元組長度|資料<br /><br /> 截斷的資料|以位元組為單位的資料長度<br /><br /> 以位元組為單位的資料長度|n/a<br /><br /> 01004|  
  
 當二進位 SQL 資料轉換為字元 C 資料時,源資料的每個位元組(8 位)表示為兩個 ASCII 字元。 這些字元是十六進位形式數位的 ASCII 字元表示形式。 例如,二進位00000001轉換為"01",二進制1111111轉換為"FF"。  
  
 驅動程序始終將單個字節轉換為十六進位數位對,並且使用空位元組終止字元字串。 因此,如果*BufferLength*是偶數且小於轉換數據的長度,則不使用 **TargetValuePtr*緩衝區的最後一個字節。 (轉換後的數據需要偶數位節,倒數第二個字節為空位元組,無法使用最後一個字節。  
  
> [!NOTE]  
>  禁止應用程式開發人員將二進位 SQL 資料繫結到字元 C 資料類型。 此轉換通常效率低下且速度緩慢。
