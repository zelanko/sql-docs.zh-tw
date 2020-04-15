---
title: dBASE 資料型態 :微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- DBase driver [ODBC], data types
- data types [ODBC], DBase driver
- dbase data types [ODBC]
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: a0e31e6b-d02b-4ee2-9b37-5baf6a11c0a6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 17b96ad0b6674a2d120ef46d9bfa221e8df6d140
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307689"
---
# <a name="dbase-data-types"></a>dBASE 資料類型
下表顯示了如何將 dBASE 數據類型映射到 ODBC SQL 資料類型。 請注意,並非所有 ODBC SQL 資料類型都受支援。  
  
|dBASE 資料類型|ODBC 資料類型|  
|---------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|日期|SQL_DATE|  
|浮點[1]|SQL_DOUBLE|  
|邏輯|SQL_BIT|  
|備忘錄|SQL_LONGVARCHAR|  
|數位 (BCD)|SQL_DOUBLE|  
|OLEOBJECT[1]|SQL_LONGBINARY|  
  
 [1] 僅適用於 dBASE 版本 5。*x*  
  
 dBASE III 中的精度允許具有最多兩位指數的數位,以及最多三位指數的 dBASE IV 數位。 由於數位存儲為文本,因此它們將轉換為數位。 如果要轉換的數位不適合欄位,則可能會出現無法解釋的結果。  
  
 雖然 dBASE 允許使用 NUMERIC 數據類型指定精度和比例,但 ODBC dBASE 驅動程式不支援它。 ODBC dBASE 驅動程式始終返回數位數據類型的精度為15和0的比例。  
  
 使用 ODBC dBASE 驅動程式創建的使用數位數據類型創建的列映射到 SQL_DOUBLE ODBC 數據類型。 因此,此列中的數據需要四捨五入。 此行為與 dBASE(類型 N)中的數位資料類型不同,後者為二進位編碼十進制十進制 (BCD)。  
  
> [!NOTE]  
>  **SQLGetTypeInfo**傳回 ODBC SQL 資料類型。 本主題前面列出的 ODBC SQL 資料類型都支援*ODBC 程式師參考*附錄 D 中的所有轉換。  
  
 下表顯示了對 dBASE 數據類型的限制。  
  
|資料類型|描述|  
|---------------|-----------------|  
|CHAR|創建零或未指定長度的 CHAR 列實際上返回 254 位元組列。|  
|加密的資料|dBASE 驅動程式不支援加密的 dBASE 表。|  
|邏輯|dBASE 驅動程式無法在「邏輯」列上創建索引。|  
|備忘錄|MEMO 列的最大長度為 65,500 位元組。|  
  
 數據類型的更多限制可以在[數據類型限制](../../odbc/microsoft/data-type-limitations.md)中找到。
