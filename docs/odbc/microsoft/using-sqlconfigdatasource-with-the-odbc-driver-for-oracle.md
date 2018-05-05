---
title: 使用 Oracle 的 ODBC 驅動程式 SQLConfigDatasource |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], ODBC driver for Oracle
ms.assetid: e535d1ef-aff9-4ae7-a3ed-ef4ca2584289
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5859b6cc446e74c12b2fb09436246d693a3beea3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="using-sqlconfigdatasource-with-the-odbc-driver-for-oracle"></a>使用 Oracle 的 ODBC 驅動程式 SQLConfigDatasource
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用由 Oracle 提供的 ODBC 驅動程式。  
  
 下表列出有效**SQLConfigDatasource** Microsoft ODBC Driver for Oracle 版本 1.0 (Msorcl10.dll) 和 Microsoft ODBC Driver for Oracle 版本 2.0 (Msorcl32.dll) 設定。  
  
> [!NOTE]  
>  Msorcl10.dll 驅動程式 （1.0 版） 支援的所有設定，除非**伺服器**。 Msorcl32.dll 驅動程式 （版本 2.0 和更新版本） 支援的所有設定。  
  
 驅動程式會忽略某些設定，但接受**SQLConfigDatasource**。 ODBC 連接字串中包含這些設定是將會接受在執行階段的唯一方式。 略過的設定不會儲存在登錄中時**SQLConfigDatasource**會建立資料來源。  
  
 下表中*A/N*表示任何有效的英數字元字串，最大容許長度。 *最大長度*（最大長度） 是設定，包括字串結束字元所接受的最大可允許的字串長度。  
  
|設定|最大長度|預設值|有效的值|Description|  
|-------------|-------------|-------------------|------------------|-----------------|  
|BufferSize|7|65535|1000|最小的提取緩衝區大小最多 65535 位元組上限|  
|CatalogCap|2|1|0 或 1|如果是 1，nonquoted 的識別項會轉換為大寫目錄中的函式。|  
|ConnectString|128|""|A/N|連接字串。 指定伺服器名稱與 Msorcl10.dll 驅動程式所需的方法。|  
|Description|256|""|A/N|描述|  
|DSN|33|""|A/N|資料來源名稱。|  
|GuessTheColDef|4|0|A/N|傳回非零值沒有 Oracle 定義小數位數的資料行。|  
|NumberFloat|2|""|0 或 1|如果為 0，浮點數資料行視為 SQL_FLOAT。 如果是 1，浮點數資料行視為 SQL_DOUBLE。|  
|PWD|30|""|A/N|密碼。|  
|RDOSupport|2|""|0 或 1|可讓 RDO 呼叫 Oracle 程序。|  
|備註|2|0|0 或 1|目錄函式中包含註解。|  
|RowLimit|4|""|0 到 99 之間|SELECT 陳述式所傳回的資料列的數目上限。 零長度字串，表示會套用任何限制。|  
|Server|128|""|A/N|Oracle 伺服器名稱。|  
|SynonymColumns|2|1|0 或 1|納入 SQLColumns 同義字。|  
|SystemTable|2|""|0 或 1|如果為 0，不會顯示系統資料表。 如果是 1，將會顯示系統資料表。|  
|TranslationDLL|33|""|A/N|轉譯.dll 名稱。|  
|TranslationName|33|""|A/N|翻譯的名稱。|  
|TranslationOption|33|""|A/N|轉譯選項。|  
|TxnCap|2|""|A/N|交易支援。 如果為 0，此驅動程式會報告不支援交易。 如果是 1，驅動程式會報告它能夠執行的交易。|  
|UID|30|""|A/N|使用者名稱。|
