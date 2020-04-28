---
title: 使用 SQLConfigDatasource 搭配 ODBC Driver for Oracle |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 718e444d63e0d4cf3821c0c03eb851732ed5b4e4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81292768"
---
# <a name="using-sqlconfigdatasource-with-the-odbc-driver-for-oracle"></a>搭配使用 SQLConfigDatasource 與 ODBC Driver for Oracle
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 所提供的 ODBC 驅動程式。  
  
 下表列出適用于 Oracle 的 Microsoft ODBC 驅動程式、版本1.0 （Msorcl10）和 Microsoft ODBC Driver for Oracle 版本2.0 （Msorcl32 .dll）的有效**SQLConfigDatasource**設定。  
  
> [!NOTE]  
>  Msorcl10 驅動程式（版本1.0）支援**Server**以外的所有設定。 Msorcl32 驅動程式（2.0 版和更新版本）支援所有設定。  
  
 驅動程式會忽略某些設定，但**SQLConfigDatasource**會接受。 將這些設定包含在 ODBC 連接字串中，是它們在執行時間接受的唯一方法。 當**SQLConfigDatasource**建立資料來源時，忽略的設定將不會儲存在登錄中。  
  
 在下表中， *A/N*表示任何有效的英數位元字串，最多可達允許的最大長度。 *Max Len* （最大長度）是設定所接受的最大允許字串長度，包括字串結束字元字元。  
  
|設定|最大長度|預設值|有效值|描述|  
|-------------|-------------|-------------------|------------------|-----------------|  
|BufferSize|7|65535|1000|最小提取緩衝區大小（最多65535個位元組）|  
|CatalogCap|2|1|0 或 1|如果是1，nonquoted 識別碼會在目錄函式中轉換成大寫。|  
|ConnectString|128|""|A/N|連接字串。 指定伺服器名稱與 Msorcl10 驅動程式的必要方法。|  
|描述|256|""|A/N|描述|  
|DSN|33|""|A/N|資料來源名稱。|  
|GuessTheColDef|4|0|A/N|針對沒有 Oracle 定義小數值的資料行傳回非零值。|  
|NumberFloat|2|""|0 或 1|如果是0，則會將 FLOAT 資料行視為 SQL_FLOAT。 如果是1，則會將 FLOAT 資料行視為 SQL_DOUBLE。|  
|PWD|30|""|A/N|密碼。|  
|RDOSupport|2|""|0 或 1|允許 RDO 呼叫 Oracle 程式。|  
|備註|2|0|0 或 1|在目錄函數中包含備註。|  
|RowLimit|4|""|0到99|SELECT 語句所傳回的最大資料列數目。 長度為零的字串表示未套用任何限制。|  
|Server (伺服器)|128|""|A/N|Oracle 伺服器名稱。|  
|SynonymColumns|2|1|0 或 1|在 SQLColumns 中包含同義字。|  
|SystemTable|2|""|0 或 1|如果為0，則不會顯示系統資料表。 如果是1，則會顯示系統資料表。|  
|TranslationDLL|33|""|A/N|轉譯 .dll 名稱。|  
|TranslationName|33|""|A/N|翻譯名稱。|  
|TranslationOption|33|""|A/N|轉譯選項。|  
|TxnCap|2|""|A/N|可支援交易。 如果是0，則驅動程式會報告它不支援交易。 如果是1，驅動程式會報告它能夠執行交易。|  
|UID|30|""|A/N|使用者名稱。|
