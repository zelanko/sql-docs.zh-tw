---
title: 桌面資料庫驅動程式的效能問題 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], performance
- desktop database drivers [ODBC], performance
- Jet-based ODBC drivers [ODBC], performance
ms.assetid: 1a4c4b7e-9744-411f-9b6e-06dfdad92cf7
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 760cec404f274d77d5382a3d164898c95545894e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="desktop-database-driver-performance-issues"></a>桌面資料庫驅動程式的效能問題
若要確保相容性與現有的 ANSI 應用程式，SQL_WCHAR、 SQL_WVARCHAR 和 SQL_WLONGVARCHAR 資料類型會公開為 SQL_CHAR、 SQL_VARCHAR 和 SQL_LONGVARCHAR Microsoft 存取 4.0 或更高的資料來源。 資料來源不會傳回寬 CHAR 資料類型，但仍然必須傳送資料至 Jet 寬字元格式。 請務必了解是否 SQL_CHAR 資料型別 ANSI 應用程式中繫結 SQL_C_CHAR 參數或結果資料行轉換將會發生。  
  
 SQL_C_CHAR 類型繫結至類型 LONGVARCHAR 的參數時，這種轉換可能會就記憶體而言，特別是沒有效率。 由於 Jet 4.0 引擎無法寫入資料流長文字參數資料，UNICODE 轉換緩衝區必須配置兩次 ANSI SQL_C_CHAR 緩衝區的大小。 應用程式執行 UNICODE 轉換，並將參數繫結 SQL_C_WCHAR 類型是最有效率的機制。 當參數標示為資料在執行，且 SQLPutData 至多個呼叫中提供的資料時，長文字資料緩衝區是增長。 其中一種方式以避免的成長這費用 」 將資料 「 緩衝區是提供 SQL_DATA_AT_EXEC_LEN(x)，透過選擇性長度其中*x*是預期的長度的位元組。 這將會初始化內部 PutData 緩衝區的大小*x*位元組。  
  
> [!NOTE]  
>  可以使用來達成有效率的方式來插入或更新長資料**SQLBulkOperations()** 或**SQLSetPos()** 以及長資料設定為 SQL_DATA_AT_EXEC。 （EXEC_LEN 會忽略在此情況下。）可以在區塊串流資料，藉由呼叫**SQLPutData**多次，這會有效地將資料附加至資料表。  
  
 當應用程式使用 Microsoft ODBC 桌面資料庫驅動程式透過 Jet 3.5 資料庫升級為 4.0 版時，則可能會發生一些效能降低以及增加的工作集大小。 這是因為當第 3 版。*x*使用新的 4.0 版驅動程式來開啟資料庫，它會載入 Jet 4.0。 當 Jet 4.0 開啟該資料庫，而會看到資料庫是 3。*x*版本，載入就相當於載入 Jet 3.5 引擎也可安裝的 ISAM 驅動程式。 若要移除的效能和大小負面影響，Jet 3。*x*應該插入 Jet 4.0 格式資料庫壓縮資料庫。 這將會消除載入兩個 Jet 引擎，並減少資料的程式碼路徑。  
  
 此外，Jet 4.0 引擎是 Unicode 引擎。 會儲存所有字串，且在 Unicode 中操作。 當 ANSI 應用程式存取 Jet 3。*x*為 Unicode，回到 ANSI，透過 Jet 4.0 引擎，資料的資料庫會從 ANSI 轉換。 如果資料庫更新至 4.0 版格式時，字串會轉換成 Unicode，移除一個層級的字串轉換，以及透過只有一個 Jet 引擎降到最低的資料的程式碼路徑。
