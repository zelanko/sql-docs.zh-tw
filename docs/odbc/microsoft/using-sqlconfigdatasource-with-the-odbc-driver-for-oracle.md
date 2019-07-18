---
title: 搭配使用 SQLConfigDatasource 與 ODBC Driver for Oracle |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], ODBC driver for Oracle
ms.assetid: e535d1ef-aff9-4ae7-a3ed-ef4ca2584289
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fa5f1ecf9f3100480081e3744fc7d280a4da282b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088029"
---
# <a name="using-sqlconfigdatasource-with-the-odbc-driver-for-oracle"></a>搭配使用 SQLConfigDatasource 與 ODBC Driver for Oracle
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用所提供的 ODBC 驅動程式。  
  
 下表列出有效**SQLConfigDatasource** Microsoft ODBC Driver for Oracle，版本 1.0 (Msorcl10.dll) 及 Microsoft ODBC Driver for Oracle (Msorcl32.dll) 2.0 版的設定。  
  
> [!NOTE]  
>  Msorcl10.dll 驅動程式 （1.0 版） 支援的所有設定，除非**Server**。 Msorcl32.dll 驅動程式 （2.0 版及更新版本） 支援所有的設定。  
  
 驅動程式會忽略某些設定，但會接受**SQLConfigDatasource**。 ODBC 連接字串中包括這些設定是將在執行階段會接受的唯一方式。 已忽略的設定不會儲存在登錄中時**SQLConfigDatasource**建立資料來源。  
  
 下表中， *A/N*表示任何有效的英數字元字串，最多允許的長度上限。 *最大 Len* （最大長度） 是設定，包括字串結束字元所接受的最大允許的字串長度。  
  
|設定|最大長度|預設值|有效的值|描述|  
|-------------|-------------|-------------------|------------------|-----------------|  
|BufferSize|7|65535|1000|最小的提取緩衝區大小最多 65535 個位元組|  
|CatalogCap|2|1|0 或 1|如果是 1，nonquoted 的識別碼會轉換成大寫字母的目錄中的函式。|  
|ConnectString|128|""|A/N|連接字串。 指定伺服器名稱與 Msorcl10.dll 驅動程式的所需的方法。|  
|描述|256|""|A/N|描述|  
|DSN|33|""|A/N|資料來源名稱。|  
|GuessTheColDef|4|0|A/N|傳回沒有 Oracle 定義小數位數的資料行的非零值。|  
|NumberFloat|2|""|0 或 1|如果為 0，浮點數資料行視為 SQL_FLOAT。 如果是 1，浮點數資料行視為 SQL_DOUBLE。|  
|PWD|30|""|A/N|密碼。|  
|RDOSupport|2|""|0 或 1|可讓 RDO 呼叫 Oracle 程序。|  
|備註|2|0|0 或 1|目錄函式中包含註解。|  
|RowLimit|4|""|0 到 99 之間|SELECT 陳述式所傳回的資料列的數目上限。 長度為零的字串表示會套用任何限制。|  
|伺服器|128|""|A/N|Oracle 伺服器名稱。|  
|SynonymColumns|2|1|0 或 1|納入 SQLColumns 同義字。|  
|SystemTable|2|""|0 或 1|如果為 0，不會顯示系統資料表。 如果是 1，將會顯示系統資料表。|  
|TranslationDLL|33|""|A/N|轉譯.dll 名稱。|  
|TranslationName|33|""|A/N|轉譯的名稱。|  
|TranslationOption|33|""|A/N|轉譯選項。|  
|TxnCap|2|""|A/N|交易支援。 如果為 0，則驅動程式會報告它不支援交易。 如果是 1，驅動程式會報告，就能夠執行的交易。|  
|UID|30|""|A/N|使用者名稱。|
