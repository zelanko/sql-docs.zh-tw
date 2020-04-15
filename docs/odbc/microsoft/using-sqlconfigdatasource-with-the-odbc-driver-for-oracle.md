---
title: 將 SQLConfigDatasource 與 Oracle 的 ODBC 驅動程式結合使用 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292768"
---
# <a name="using-sqlconfigdatasource-with-the-odbc-driver-for-oracle"></a>搭配使用 SQLConfigDatasource 與 ODBC Driver for Oracle
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 而是使用 Oracle 提供的 ODBC 驅動程式。  
  
 下表列出了適用於 Oracle 的 Microsoft ODBC 驅動程式、版本 1.0(Msorcl10.dll) 和 Oracle 的 Microsoft ODBC 驅動程式(2.0 版(Msorcl32.dll)的有效**SQLConfigDatasource**設置。  
  
> [!NOTE]  
>  Msorcl10.dll 驅動程式(版本 1.0)支援**除伺服器**之外的所有設置。 Msorcl32.dll 驅動程式(版本 2.0 及以上)支援所有設置。  
  
 某些設置被驅動程式忽略,但**SQLConfigDatasource**接受。 在 ODBC 連接字串中包含這些設定是運行時接受這些設置的唯一方法。 **當 SQLConfigDatasource**建立資料來源時,忽略的設定將不會儲存在註冊表中。  
  
 在下表中 *,A/N*表示任何有效的字母數位字串,最長可達允許長度。 *最大 Len(* 最大長度) 是設定接受的最大允許字串長度,包括字串終結器字元。  
  
|設定|馬克斯·倫|預設值|有效值|描述|  
|-------------|-------------|-------------------|------------------|-----------------|  
|BufferSize|7|65535|1000|最小擷取緩衝區大小高達 65535 位元組|  
|目錄帽|2|1|0 或 1|如果為 1,則非引號識別符將在目錄函數中轉換為大寫。|  
|ConnectString|128|""|A/N|連接字串。 使用 Msorcl10.dll 驅動程式指定伺服器名稱的必需方法。|  
|描述|256|""|A/N|描述|  
|DSN|33|""|A/N|數據源名稱。|  
|猜謎|4|0|A/N|為沒有 Oracle 定義的比例的列返回非零值。|  
|數量浮動|2|""|0 或 1|如果為 0,則 FLOAT 列將被視為SQL_FLOAT。 如果為 1,則 FLOAT 列將被視為SQL_DOUBLE。|  
|PWD|30|""|A/N|密碼。|  
|RDO支援|2|""|0 或 1|允許 RDO 呼叫 Oracle 過程。|  
|備註|2|0|0 或 1|在目錄函數中包括註釋。|  
|行限制|4|""|0 到 99|SELECT 語句返回的最大行數。 零長度字串表示不應用任何限制。|  
|伺服器|128|""|A/N|Oracle 伺服器名稱。|  
|同義字列|2|1|0 或 1|在 SQL 欄中包括 SYNONYM。|  
|系統表|2|""|0 或 1|如果為 0,則不會顯示系統表。 如果為 1,則將顯示系統表。|  
|翻譯DLL|33|""|A/N|翻譯 .dll 名稱。|  
|翻譯名稱|33|""|A/N|翻譯名稱。|  
|翻譯選項|33|""|A/N|翻譯選項。|  
|TxnCap|2|""|A/N|事務能力。 如果為 0,驅動程式將報告它不支援事務。 如果為 1,則驅動程序報告它能夠執行事務。|  
|UID|30|""|A/N|使用者名稱。|
