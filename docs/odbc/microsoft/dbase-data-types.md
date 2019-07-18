---
title: dBASE 資料類型 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1753e0d50655205bc6f459548f2ef2b77d5cc885
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096456"
---
# <a name="dbase-data-types"></a>dBASE 資料類型
下表顯示 dBASE 資料類型如何對應至 ODBC SQL 資料類型。 請注意，並非所有的 ODBC SQL 資料類型所支援。  
  
|dBASE 資料類型|ODBC 資料類型|  
|---------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATE|SQL_DATE|  
|FLOAT[1]|SQL_DOUBLE|  
|邏輯|SQL_BIT|  
|附註|SQL_LONGVARCHAR|  
|數值 (BCD)|SQL_DOUBLE|  
|OLEOBJECT [1]|SQL_LONGBINARY|  
  
 [1] 只會針對 dBASE 第 5 版的有效。*x*  
  
 DBASE 的有效位數 III 允許數字與設定兩位數指數，dBASE IV 的數字中最多三位數指數。 因為數字會儲存為文字，所以會轉換成數字。 如果要轉換的數字不適合在欄位中，可能會發生無法解釋的結果。  
  
 有效位數和小數位數來指定具有數值資料類型，可讓 dBASE，它不是支援 ODBC dBASE 驅動程式。 ODBC dBASE 驅動程式一律會傳回 15 個有效位數和小數位數 0 的數值資料類型。  
  
 建立與使用 ODBC dBASE 驅動程式會對應至 ODBC SQL_DOUBLE 資料類型的數值資料類型的資料行。 因此，此資料行中的資料是受制於捨入。 這個行為並不相同的數值資料輸入 dBASE （類型 N），在這是 Binary Coded Decimal (BCD)。  
  
> [!NOTE]  
>  **SQLGetTypeInfo**傳回 ODBC SQL 資料類型。 附錄 D 中的所有轉換*ODBC 程式設計人員參考*稍早在本主題中列出的 ODBC SQL 資料類型支援。  
  
 下表顯示限制在 dBASE 資料類型。  
  
|資料類型|描述|  
|---------------|-----------------|  
|CHAR|建立 CHAR 資料行的零或未指定的長度實際上會傳回 254 個位元組的資料行。|  
|加密的資料|DBASE 驅動程式不支援加密的 dBASE 資料表。|  
|邏輯|DBASE 驅動程式無法在邏輯資料行上建立索引。|  
|附註|備忘資料行的最大長度是 65,500 個位元組。|  
  
 資料型別上的更多限制可在[資料型別限制](../../odbc/microsoft/data-type-limitations.md)。
