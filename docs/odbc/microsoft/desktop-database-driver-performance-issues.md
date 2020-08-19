---
description: 桌面資料庫驅動程式效能問題
title: 桌面資料庫驅動程式效能問題 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], performance
- desktop database drivers [ODBC], performance
- Jet-based ODBC drivers [ODBC], performance
ms.assetid: 1a4c4b7e-9744-411f-9b6e-06dfdad92cf7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 20c21c493d81df6afb4a338675f86ad96ccfab68
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449550"
---
# <a name="desktop-database-driver-performance-issues"></a>桌面資料庫驅動程式效能問題
為了確保與現有的 ANSI 應用程式相容，SQL_WCHAR、SQL_WVARCHAR 和 SQL_WLONGVARCHAR 資料類型會公開為 Microsoft Access 4.0 或更高版本的資料來源 SQL_CHAR、SQL_VARCHAR 和 SQL_LONGVARCHAR。 資料來源不會傳回寬 CHAR 資料類型，但仍必須將資料傳送到寬字元格式的 Jet。 請務必瞭解，如果 SQL_C_CHAR 參數或結果資料行系結至 ANSI 應用程式中的 SQL_CHAR 資料類型，就會進行轉換。  
  
 當 SQL_C_CHAR 類型系結至 LONGVARCHAR 類型的參數時，這項轉換在記憶體方面可能特別沒有效率。 由於 Jet 4.0 引擎無法串流 LONGTEXT 參數資料，因此必須配置 UNICODE 轉換緩衝區，這是 SQL_C_CHAR ANSI 緩衝區大小的兩倍。 最有效率的機制是讓應用程式執行 UNICODE 轉換，然後將參數系結為類型 SQL_C_WCHAR。 當參數標示為數據執行中，且在多個 SQLPutData 呼叫中提供資料時，會增加 longtext 資料緩衝區。 若要避免增加這個「Put 資料」緩衝區的費用，其中一個方法是透過 SQL_DATA_AT_EXEC_LEN (x) 提供選擇性的長度，其中 *x* 是預期的位元組長度。 這會將內部 PutData 緩衝區的大小初始化為 *x* 個位元組。  
  
> [!NOTE]  
>  您可以使用 **SQLBulkOperations ( # B1 ** 或 **SQLSetPos ( # B3 ** 並將長資料設定為 SQL_DATA_AT_EXEC，以有效率的方式來插入或更新 long 資料。 在此情況下，會忽略 (的 EXEC_LEN ) 。您可以多次呼叫 **SQLPutData** ，將資料分割成區塊，如此就能有效地將資料附加至資料表。  
  
 當透過 Microsoft ODBC Desktop 資料庫驅動程式使用 Jet 3.5 資料庫的應用程式升級至4.0 版時，可能會有一些效能降低，而且可能會發生更大的工作集大小。 這是因為第3版。*x* 資料庫是使用新的4.0 版驅動程式來開啟，它會載入 Jet 4.0。 當 Jet 4.0 開啟資料庫時，會看到資料庫是3。*x* 版，它會載入一個可安裝的 ISAM 驅動程式，也就是載入 Jet 3.5 引擎。 為了移除效能和大小的負面影響，Jet 3。*x* 資料庫應壓縮成 Jet 4.0 格式資料庫。 這會排除載入兩個 Jet 引擎，並將資料的程式碼路徑降至最低。  
  
 此外，Jet 4.0 引擎也是 Unicode 引擎。 所有字串都會以 Unicode 儲存和操作。 當 ANSI 應用程式存取 Jet 3 時。透過 Jet 4.0 引擎的*x* 資料庫，資料會從 ANSI 轉換成 Unicode，然後再轉換回 ansi。 如果資料庫更新為4.0 格式，則會將字串轉換成 Unicode，移除一個層級的字串轉換，以及藉由只執行一個 Jet 引擎來將程式碼路徑降至最低。
