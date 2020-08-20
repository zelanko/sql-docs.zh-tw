---
description: Microsoft Excel 資料類型
title: Microsoft Excel 資料類型 |Microsoft Docs
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
ms.openlocfilehash: b3e54ece7962fc5b56e4b9fcc17123ac7ad3c9e8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466430"
---
# <a name="microsoft-excel-data-types"></a>Microsoft Excel 資料類型
下表說明 Microsoft Excel 驅動程式資料類型如何對應至 ODBC SQL 資料類型。 Microsoft Excel 驅動程式會根據資料行中的資料，將這些資料類型指派給 Microsoft Excel 資料表中的資料行。  
  
|Microsoft Excel 資料類型|ODBC 資料類型|  
|-------------------------------|--------------------|  
|CURRENCY|SQL_NUMERIC|  
|DATETIME|SQL_TIMESTAMP|  
|邏輯|SQL_BIT|  
|NUMBER|SQL_DOUBLE|  
|TEXT|SQL_VARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** 會傳回 ODBC SQL 資料類型。 本主題稍早所列的 ODBC SQL 資料類型支援 Odbc 程式設計 *人員參考* 附錄 D 中的所有轉換。  
  
 下表顯示 Microsoft Excel 資料類型的限制。  
  
|資料類型|描述|  
|---------------|-----------------|  
|加密的資料|Microsoft Excel 驅動程式無法讀取加密的資料。|  
|錯誤字串|Microsoft Excel 驅動程式無法傳回 Microsoft Excel 錯誤值的字元字串 ( # N/A！、#VALUE！、#REF！、#DIV/0！、#NUM！、#NAME？和 #Null！ ) ，但改為傳回 Null。|  
|邏輯|邏輯資料行中的值會在 SQL_C_CHAR 緩衝區中傳回0或1。|  
|NUMBER|如果建立了整數資料行，就可以輸入對整數資料類型而言太大的數位，而且可以插入包含非整數值的資料，結果會將資料行轉換成 SQL_DOUBLE。|  
|TEXT|當資料行的資料列包含一個以上的 Microsoft Excel 資料類型時，ODBC Microsoft Excel 驅動程式會將 SQL_VARCHAR 資料類型指派給資料行。 有一個例外狀況：如果資料行只包含兩個或三個 datetime 資料類型 (DATE、TIME 和 DATETIME) ，ODBC Microsoft Excel 驅動程式會將 SQL_TIMESTAMP 資料類型指派給資料行。<br /><br /> 建立零或未指定長度的文字資料行，實際上會傳回255個位元組的資料行。<br /><br /> 字元字串常值可以包含任何 (1-255 decimal) 的 ANSI 字元。 使用兩個連續的單引號 ( ") 表示 ( ' ) 的一個單引號。<br /><br /> 將 Null 插入資料類型不是 SQL_VARCHAR 的資料行，將會導致資料行的資料類型變更為 SQL_VARCHAR。|  
  
 您可以在 [資料類型限制](../../odbc/microsoft/data-type-limitations.md)中找到更多有關資料類型的限制。
