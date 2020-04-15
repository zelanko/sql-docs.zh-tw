---
title: 微軟存取資料類型 |微軟文件
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
- Access driver [ODBC], data types
- access data types [ODBC]
- data types [ODBC], Access driver
ms.assetid: b537348a-bea0-4bd6-84a4-52a75292957f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 024fb65b6fdc81ae0a8e007d1cee150c6a35b91c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307727"
---
# <a name="microsoft-access-data-types"></a>Microsoft Access 資料類型
下表顯示了 Microsoft Access 數據類型、用於建立表的數據類型和 ODBC SQL 資料類型。  
  
|微軟存取資料類型|資料型態(建立表)|ODBC SQL 資料類型|  
|--------------------------------|-------------------------------|------------------------|  
|大二進位[1]|長二進位|SQL_LONGVARBINARY|  
|BINARY|BINARY|SQL_BINARY|  
|BIT|BIT|SQL_BIT|  
|計數器|計數器|SQL_INTEGER|  
|CURRENCY|CURRENCY|SQL_NUMERIC|  
|日期/時間|DATETIME|SQL_TIMESTAMP|  
|GUID|GUID|SQL_GUID|  
|長二進位|長二進位|SQL_LONGVARBINARY|  
|長文字|長文字|SQL_LONGVARCHAR[2] SQL_WLONGVARCHAR[3]|  
|備忘錄|長文字|SQL_LONGVARCHAR[2] SQL_WLONGVARCHAR[3]|  
|編號(欄位大小= 單)|單|SQL_REAL|  
|編號(欄位大小= 雙)|DOUBLE|SQL_DOUBLE|  
|編號(欄位大小= 位元組)|未簽名名字|SQL_TINYINT|  
|數量(欄位大小= 整數 )|SHORT|SQL_SMALLINT|  
|數量(欄位大小= 長整數 )|LONG|SQL_INTEGER|  
|NUMERIC|NUMERIC|SQL_NUMERIC|  
|OLE|長二進位|SQL_LONGVARBINARY|  
|TEXT|VARCHAR|SQL_VARCHAR[1] SQL_WVARCHAR[2]|  
|VARBINARY|VARBINARY|SQL_VARBINARY|  
  
 [1] 僅訪問 4.0 應用程式。 最大長度為 4000 位元組。 類似於 LONGBINARY 的行為。  
  
 [2] 僅限 ANSI 應用程式。  
  
 [3] 僅 Unicode 和訪問 4.0 應用程式。  
  
> [!NOTE]  
>  **SQLGetTypeInfo**傳回 ODBC 資料類型。 如果將多個 Microsoft Access 類型映射到相同的 ODBC SQL 資料類型,則不會返回所有 Microsoft Access 數據類型。 對於上表中列出的 SQL 資料類型,支援*ODBC 程式師參考*附錄 D 中的所有轉換。  
  
 下表顯示了對 Microsoft Access 數據類型的限制。  
  
|資料類型|描述|  
|---------------|-----------------|  
|BINARY、VARBINARY 和 VARCHAR|創建零或未指定長度的 BINARY、VARBINARY 或 VARCHAR 列實際上返回一個 510 位元組的列。|  
|BYTE|即使欄位大小等於 BYTE 的 Microsoft 存取編號欄位是無符號的,但在使用 Microsoft Access 驅動程式時,也可以將負數插入到該欄位中。|  
|查爾、朗瓦爾查爾和瓦爾查爾|字串文字可以包含任何 ANSI 字元(1-255 位小數)。 使用兩個連續的單引號 ('') 表示一個單引號 (')。<br /><br /> 在字元數據類型列中使用任何特殊字元時,應使用過程來傳遞字元數據。|  
|日期|日期值必須根據 ODBC 規範日期格式進行分隔,或者由日期時間分隔符 ("*")分隔。 否則,Microsoft Access 會將該值視為算術表達式,不會引發警告或錯誤。<br /><br /> 例如,"1996年3月5日"的日期必須表示為[d'1996-03-05']或#03/05/1996];否則,如果只提交 03/05/1993,Microsoft Access 將對此進行評估為 3 除以 5 除以 1996。 此值舍入到整數 0,並且由於零日映射到 1899-12-31,這是使用的日期。<br /><br /> 管道字元 (&#124;) 不能用於日期值,即使包含在後引號中也是如此。|  
|GUID|數據類型僅限於Microsoft存取4.0。|  
|NUMERIC|數據類型僅限於Microsoft存取4.0。|  
  
 數據類型的更多限制可以在[數據類型限制](../../odbc/microsoft/data-type-limitations.md)中找到。
