---
title: Microsoft Access 資料類型 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3ff069ef0602e419eda93df0ca5a72dbf7c8ef1e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68045166"
---
# <a name="microsoft-access-data-types"></a>Microsoft Access 資料類型
下表顯示 Microsoft Access 資料類型、用來建立資料表的資料類型，以及 ODBC SQL 資料類型。  
  
|Microsoft Access 資料類型|資料類型（CREATETABLE）|ODBC SQL 資料類型|  
|--------------------------------|-------------------------------|------------------------|  
|BIGBINARY [1]|LONGBINARY|SQL_LONGVARBINARY|  
|BINARY|BINARY|SQL_BINARY|  
|BIT|BIT|SQL_BIT|  
|抵禦|抵禦|SQL_INTEGER|  
|CURRENCY|CURRENCY|SQL_NUMERIC|  
|日期/時間|DATETIME|SQL_TIMESTAMP|  
|GUID|GUID|SQL_GUID|  
|長二進位|LONGBINARY|SQL_LONGVARBINARY|  
|長文字|LONGTEXT|SQL_LONGVARCHAR [2] SQL_WLONGVARCHAR [3]|  
|備忘|LONGTEXT|SQL_LONGVARCHAR [2] SQL_WLONGVARCHAR [3]|  
|數位（FieldSize = SINGLE）|單機|SQL_REAL|  
|數位（FieldSize = DOUBLE）|DOUBLE|SQL_DOUBLE|  
|數位（FieldSize = BYTE）|不帶正負號的位元組|SQL_TINYINT|  
|NUMBER （FieldSize = INTEGER）|短缺|SQL_SMALLINT|  
|數位（FieldSize = LONG 整數）|LONG|SQL_INTEGER|  
|NUMERIC|NUMERIC|SQL_NUMERIC|  
|OLE|LONGBINARY|SQL_LONGVARBINARY|  
|TEXT|VARCHAR|SQL_VARCHAR [1] SQL_WVARCHAR [2]|  
|VARBINARY|VARBINARY|SQL_VARBINARY|  
  
 [1] 僅存取4.0 應用程式。 長度上限為4000個位元組。 類似于 LONGBINARY 的行為。  
  
 [2] 僅限 ANSI 應用程式。  
  
 [3] Unicode 並僅存取4.0 應用程式。  
  
> [!NOTE]  
>  **SQLGetTypeInfo**會傳回 ODBC 資料類型。 如果有一或多個 Microsoft 存取類型對應至相同的 ODBC SQL 資料類型，則不會傳回所有的 Microsoft Access 資料類型。 針對上表所列的 SQL 資料類型，支援 ODBC 程式設計*人員參考*附錄 D 中的所有轉換。  
  
 下表顯示 Microsoft Access 資料類型的限制。  
  
|資料類型|描述|  
|---------------|-----------------|  
|BINARY、VARBINARY 和 VARCHAR|建立零或未指定長度的 BINARY、VARBINARY 或 VARCHAR 資料行時，實際上會傳回510位元組的資料行。|  
|BYTE|雖然 FieldSize 等於 BYTE 的 Microsoft Access NUMBER 欄位不帶正負號，但使用 Microsoft Access 驅動程式時，可以將負數插入欄位中。|  
|CHAR、LONGVARCHAR 和 VARCHAR|字元字串常值可以包含任何 ANSI 字元（1-255 十進位）。 使用兩個連續的單引號（' '）來代表一個單引號（'）。<br /><br /> 使用字元資料類型資料行中的任何特殊字元時，應該使用程式來傳遞字元資料。|  
|日期|日期值必須根據 ODBC 標準日期格式來分隔，或以日期時間分隔符號（"#"）分隔。 否則，Microsoft Access 會將此值視為算術運算式，而且不會引發警告或錯誤。<br /><br /> 例如，日期「3月5日，1996」必須以 {d ' 1996-03-05 '} 或 #03/05/1996 # 表示。否則，如果只提交03/05/1993，Microsoft Access 會將此值評估為3除以5除以1996。 這個值會無條件進位到整數0，而且因為零日對應到1899-12-31，所以這是使用的日期。<br /><br /> 即使以後引號括住，也不能在日期值中使用管線字元（&#124;）。|  
|GUID|資料類型限制為 Microsoft Access 4.0。|  
|NUMERIC|資料類型限制為 Microsoft Access 4.0。|  
  
 您可以在[資料類型限制](../../odbc/microsoft/data-type-limitations.md)中找到更多有關資料類型的限制。
