---
description: dBASE 資料類型
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9eca7d603a136bd1921ee93656d38f59efcda5f4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412764"
---
# <a name="dbase-data-types"></a>dBASE 資料類型
下表說明 dBASE 資料類型如何對應至 ODBC SQL 資料類型。 請注意，並非所有的 ODBC SQL 資料類型都受到支援。  
  
|dBASE 資料類型|ODBC 資料類型|  
|---------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|日期|SQL_DATE|  
|FLOAT [1]|SQL_DOUBLE|  
|邏輯|SQL_BIT|  
|備忘錄|SQL_LONGVARCHAR|  
|數值 (BCD) |SQL_DOUBLE|  
|OLEOBJECT [1]|SQL_LONGBINARY|  
  
 [1] 只適用于 dBASE 版本5。*x*  
  
 DBASE III 中的有效位數允許最多有兩位數指數的數位，以及最多三位數指數的 dBASE IV 數位。 因為數位會儲存為文字，所以會轉換成數位。 如果要轉換的數位不符合欄位，可能會發生無法解釋的結果。  
  
 雖然 dBASE 允許使用數值資料類型指定有效位數和小數位數，但是 ODBC dBASE 驅動程式並不支援。 針對數值資料類型，ODBC dBASE 驅動程式一律會傳回15的有效位數，且小數位數為0。  
  
 使用 ODBC dBASE 驅動程式所建立之數值資料類型的資料行，會對應至 SQL_DOUBLE ODBC 資料類型。 因此，此資料行中的資料可能會進行四捨五入。 這種行為與 dBASE 中數值資料類型的行為不同 (類型 N) ，也就是二進位編碼的十進位 (BCD) 。  
  
> [!NOTE]  
>  **SQLGetTypeInfo** 會傳回 ODBC SQL 資料類型。 本主題稍早所列的 ODBC SQL 資料類型支援 Odbc 程式設計 *人員參考* 附錄 D 中的所有轉換。  
  
 下表顯示 dBASE 資料類型的限制。  
  
|資料類型|描述|  
|---------------|-----------------|  
|CHAR|建立零或未指定長度的 CHAR 資料行實際上會傳回254個位元組的資料行。|  
|加密的資料|DBASE 驅動程式不支援加密的 dBASE 資料表。|  
|邏輯|DBASE 驅動程式無法在邏輯資料行上建立索引。|  
|備忘錄|備忘錄資料行的最大長度為65500個位元組。|  
  
 您可以在 [資料類型限制](../../odbc/microsoft/data-type-limitations.md)中找到更多有關資料類型的限制。
