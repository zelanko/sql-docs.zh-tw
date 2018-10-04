---
title: Microsoft Excel 的資料型別 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10695dd9bf044e270bb1ce1d26de78e53a1dd85a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47656756"
---
# <a name="microsoft-excel-data-types"></a>Microsoft Excel 資料類型
下表顯示如何將 Microsoft Excel 驅動程式資料類型對應至 ODBC SQL 資料類型。 Microsoft Excel 驅動程式會將這些資料類型指派給資料行中資料為基礎的 Microsoft Excel 資料表中資料行。  
  
|Microsoft Excel 資料類型|ODBC 資料類型|  
|-------------------------------|--------------------|  
|CURRENCY|SQL_NUMERIC|  
|DATETIME|SQL_TIMESTAMP|  
|邏輯|SQL_BIT|  
|NUMBER|SQL_DOUBLE|  
|TEXT|SQL_VARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo**傳回 ODBC SQL 資料類型。 附錄 D 中的所有轉換*ODBC 程式設計人員參考*稍早在本主題中列出的 ODBC SQL 資料類型支援。  
  
 下表顯示在 Microsoft Excel 的資料型別上的限制。  
  
|資料類型|描述|  
|---------------|-----------------|  
|加密的資料|Microsoft Excel 驅動程式無法讀取加密的資料。|  
|錯誤字串|Microsoft Excel 驅動程式不能傳回的字元字串的 Microsoft Excel 錯誤值 (# n/A ！，#VALUE ！，#REF ！、 #DIV/0 ！，#NUM ！，#NAME？，和 #NULL ！)，但改為傳回 null 值。|  
|邏輯|SQL_C_CHAR 緩衝區中傳回的邏輯資料行中的值為 0 或 1。|  
|NUMBER|如果整數資料行所建立，可以輸入的整數資料類型太大的數字，且包含非整數值的資料可插入的資料行，可能會轉換成 SQL_DOUBLE 結果。|  
|TEXT|當資料行的資料列包含一個以上的 Microsoft Excel 的資料類型時，ODBC Microsoft Excel 驅動程式會指派 SQL_VARCHAR 資料類型的資料行。 沒有唯一的例外： 如果資料行包含只有兩個或三個 （日期、 時間和日期時間） 時，datetime 資料類型，ODBC Microsoft Excel 驅動程式會將 SQL_TIMESTAMP 資料類型指派給資料行。<br /><br /> 建立文字資料行的零或未指定的長度實際上會傳回 255 個位元組的資料行。<br /><br /> 字元字串常值可以包含任何 ANSI 字元 （1-255 十進位）。 您可以使用兩個連續單引號 （'） 來表示一個單引號 （'）。<br /><br /> 插入資料行中的 null 值，與非 SQL_VARCHAR 資料類型會變更為 SQL_VARCHAR 資料行的資料類型。|  
  
 資料型別上的更多限制可在[資料型別限制](../../odbc/microsoft/data-type-limitations.md)。
