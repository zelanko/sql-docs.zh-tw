---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 660b7c123d0ddd0a3f1b972fa3b1dc153b15ed50
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68071935"
---
# <a name="desktop-database-driver-performance-issues"></a>桌面資料庫驅動程式效能問題
為了確保與現有 ANSI 應用程式的相容性，SQL_WCHAR、SQL_WVARCHAR 和 SQL_WLONGVARCHAR 資料類型會公開為 Microsoft Access 4.0 或更高版本資料來源的 SQL_CHAR、SQL_VARCHAR 和 SQL_LONGVARCHAR。 資料來源不會傳回寬字元資料類型，但資料仍然必須以寬字元形式傳送到 Jet。 請務必瞭解，如果 SQL_C_CHAR 參數或結果資料行系結至 ANSI 應用程式中的 SQL_CHAR 資料類型，就會發生轉換。  
  
 當 SQL_C_CHAR 類型系結至 LONGVARCHAR 類型的參數時，這項轉換可能會對記憶體造成特別的效率。 由於 Jet 4.0 引擎無法串流 LONGTEXT 參數資料，因此必須配置 UNICODE 轉換緩衝區，這是 SQL_C_CHAR ANSI 緩衝區大小的兩倍。 最有效率的機制是讓應用程式執行 UNICODE 轉換，並將參數系結為 SQL_C_WCHAR 的型別。 當參數標記為數據執行中，而且在多個 SQLPutData 呼叫中提供資料時，會增加 longtext 資料緩衝區。 若要避免此「Put 資料」緩衝區不斷增加，其中一種方法是透過 SQL_DATA_AT_EXEC_LEN （x）提供選擇性的長度，其中*x*是預期的位元組長度。 這會將內部 PutData 緩衝區的大小初始化為*x*個位元組。  
  
> [!NOTE]  
>  您可以使用**SQLBulkOperations （）** 或**SQLSetPos （）** 來完成插入或更新長資料的有效方式，並將長資料設定為 SQL_DATA_AT_EXEC。 （在此情況下，會忽略 EXEC_LEN）。藉由多次呼叫**SQLPutData** ，可將資料以區塊方式串流，這會有效地將資料附加至資料表。  
  
 透過 Microsoft ODBC 桌面資料庫驅動程式使用 Jet 3.5 資料庫的應用程式升級至4.0 版時，可能會降低效能，並增加工作集大小。 這是因為第3版。*x*資料庫是使用新版本4.0 驅動程式來開啟，它會載入 Jet 4.0。 當 Jet 4.0 開啟資料庫，並看到資料庫為3時。*x*版本，它會載入可安裝的 ISAM 驅動程式，相當於載入 Jet 3.5 引擎。 若要移除效能和大小的負面影響，Jet 3。*x*資料庫應該壓縮成 Jet 4.0 格式資料庫。 這會排除載入兩個 Jet 引擎，並將資料的程式碼路徑降至最低。  
  
 此外，Jet 4.0 引擎是 Unicode 引擎。 所有字串都會以 Unicode 儲存和操作。 當 ANSI 應用程式存取 Jet 3 時。*x*資料庫：透過 Jet 4.0 引擎，資料會從 ANSI 轉換成 Unicode，並傳回 ansi。 如果資料庫更新為版本4.0 格式，則字串會轉換成 Unicode，移除一個層級的字串轉換，並藉由只執行一個 Jet 引擎來將程式碼路徑最小化。
