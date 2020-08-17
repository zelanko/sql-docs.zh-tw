---
description: Microsoft Access 資料類型
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 24428c436e9e60c8ca5e42288b217f2c576cbd0d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340764"
---
# <a name="microsoft-access-data-types"></a>Microsoft Access 資料類型
下表顯示 Microsoft Access 資料類型、用來建立資料表的資料類型，以及 ODBC SQL 資料類型。  
  
|Microsoft Access 資料類型|資料類型 (CREATETABLE) |ODBC SQL 資料類型|  
|--------------------------------|-------------------------------|------------------------|  
|BIGBINARY [1]|LONGBINARY|SQL_LONGVARBINARY|  
|BINARY|BINARY|SQL_BINARY|  
|BIT|BIT|SQL_BIT|  
|計數器|計數器|SQL_INTEGER|  
|CURRENCY|CURRENCY|SQL_NUMERIC|  
|日期/時間|DATETIME|SQL_TIMESTAMP|  
|GUID|GUID|SQL_GUID|  
|長二進位|LONGBINARY|SQL_LONGVARBINARY|  
|長文字|LONGTEXT|SQL_LONGVARCHAR [2] SQL_WLONGVARCHAR [3]|  
|備忘錄|LONGTEXT|SQL_LONGVARCHAR [2] SQL_WLONGVARCHAR [3]|  
|NUMBER (FieldSize = SINGLE) |單|SQL_REAL|  
|NUMBER (FieldSize = DOUBLE) |DOUBLE|SQL_DOUBLE|  
|NUMBER (FieldSize = BYTE) |不帶正負號的位元組|SQL_TINYINT|  
|NUMBER (FieldSize = INTEGER) |SHORT|SQL_SMALLINT|  
|NUMBER (FieldSize = LONG INTEGER) |LONG|SQL_INTEGER|  
|NUMERIC|NUMERIC|SQL_NUMERIC|  
|OLE|LONGBINARY|SQL_LONGVARBINARY|  
|TEXT|VARCHAR|SQL_VARCHAR [1] SQL_WVARCHAR [2]|  
|VARBINARY|VARBINARY|SQL_VARBINARY|  
  
 [1] 只存取4.0 應用程式。 最大長度4000個位元組。 類似于 LONGBINARY 的行為。  
  
 [2] 僅限 ANSI 應用程式。  
  
 [3] 僅限 Unicode 和 Access 4.0 應用程式。  
  
> [!NOTE]  
>  **SQLGetTypeInfo** 會傳回 ODBC 資料類型。 如果有多個 Microsoft 存取類型對應到相同的 ODBC SQL 資料類型，則不會傳回所有的 Microsoft Access 資料類型。 上表所列的 SQL 資料類型支援 ODBC 程式設計 *人員參考* 附錄 D 中的所有轉換。  
  
 下表顯示 Microsoft Access 資料類型的限制。  
  
|資料類型|描述|  
|---------------|-----------------|  
|BINARY、VARBINARY 和 VARCHAR|建立零或未指定長度的 BINARY、VARBINARY 或 VARCHAR 資料行實際上會傳回510個位元組的資料行。|  
|BYTE|即使 Microsoft Access NUMBER 欄位的 FieldSize 等於 BYTE，也不帶正負號，但使用 Microsoft Access 驅動程式時可以將負數插入欄位中。|  
|CHAR、LONGVARCHAR 和 VARCHAR|字元字串常值可以包含任何 (1-255 decimal) 的 ANSI 字元。 請使用兩個連續的單引號 ( ' ' ) 來代表 ( ' ) 的一個單引號。<br /><br /> 使用字元資料類型資料行中的任何特殊字元時，應該使用程式來傳遞字元資料。|  
|日期|日期值必須根據 ODBC 標準日期格式來分隔，或是以 datetime 分隔符號分隔 ( "#" ) 。 否則，Microsoft Access 會將值視為算術運算式，而且不會引發警告或錯誤。<br /><br /> 例如，日期「1996年3月5日」必須表示為 {d ' 1996-03-05 '} 或 #03/05/1996 #;否則，如果只提交03/05/1993，Microsoft Access 會將其評估為3除以5除以1996。 此值會無條件進位到整數0，因為零天會對應到1899-12-31，這是使用的日期。<br /><br /> 即使以引號括住，也無法在日期值中使用管道字元 ( # A0) 。|  
|GUID|資料類型受限於 Microsoft Access 4.0。|  
|NUMERIC|資料類型受限於 Microsoft Access 4.0。|  
  
 您可以在 [資料類型限制](../../odbc/microsoft/data-type-limitations.md)中找到更多有關資料類型的限制。
