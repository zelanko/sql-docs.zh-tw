---
title: 微軟Excel數據類型 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], Excel driver
- Excel data types [ODBC]
- Jet-based ODBC drivers [ODBC], Excel driver
- desktop database drivers [ODBC], Excel driver
- ODBC desktop database drivers [ODBC], Excel driver
- Excel driver [ODBC], data types
ms.assetid: 7b44c8e5-0bc3-4912-8a5d-56f4d5562fe6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8574985e10e5aaa3ae5431af7ee1245643e20b60
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283768"
---
# <a name="microsoft-excel-data-types"></a>Microsoft Excel 資料類型
下表顯示了如何將 Microsoft Excel 驅動程式數據類型映射到 ODBC SQL 資料類型。 Microsoft Excel 驅動程式根據列中的數據將這些數據類型分配給 Microsoft Excel 表中的列。  
  
|微軟 Excel 資料類型|ODBC 資料類型|  
|-------------------------------|--------------------|  
|CURRENCY|SQL_NUMERIC|  
|DATETIME|SQL_TIMESTAMP|  
|邏輯|SQL_BIT|  
|NUMBER|SQL_DOUBLE|  
|TEXT|SQL_VARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo**傳回 ODBC SQL 資料類型。 本主題前面列出的 ODBC SQL 資料類型都支援*ODBC 程式師參考*附錄 D 中的所有轉換。  
  
 下表顯示了對 Microsoft Excel 數據類型的限制。  
  
|資料類型|描述|  
|---------------|-----------------|  
|加密的資料|Microsoft Excel 驅動程式無法讀取加密數據。|  
|錯誤字串|Microsoft Excel 驅動程式無法返回 Microsoft Excel 錯誤值(#N/A!、#VALUE!、#REF!、#DIV/0!、#NUM!、#NAME 和 #NULL!)的字串,而是返回 NULL。|  
|邏輯|"邏輯"列中的值在SQL_C_CHAR緩衝區中返回為 0 或 1。|  
|NUMBER|如果創建了整數列,則可以輸入對於整數數據類型太大的數位,並可以插入包含非整數值的數據,結果該列可以轉換為SQL_DOUBLE。|  
|TEXT|當列的行包含多個 Microsoft Excel 數據類型時,ODBC Microsoft Excel 驅動程式會將SQL_VARCHAR數據類型分配給該列。 存在一個例外:如果列僅包含兩個或三個日期時間數據類型(日期、時間和 DATETIME),則 ODBC Microsoft Excel 驅動程式將SQL_TIMESTAMP數據類型分配給列。<br /><br /> 建立零或未指定長度的 TEXT 列實際上傳回 255 位元組列。<br /><br /> 字串文字可以包含任何 ANSI 字元(1-255 位小數)。 使用兩個連續的單引號 (") 表示一個單引號 (')。<br /><br /> 將 NULL 插入具有SQL_VARCHAR以外的資料類型的欄將導致列的資料類型更改為SQL_VARCHAR。|  
  
 數據類型的更多限制可以在[數據類型限制](../../odbc/microsoft/data-type-limitations.md)中找到。
