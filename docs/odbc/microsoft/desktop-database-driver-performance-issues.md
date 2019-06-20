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
manager: craigg
ms.openlocfilehash: b4d92d2784649e4366113b3070b54598df585370
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63240309"
---
# <a name="desktop-database-driver-performance-issues"></a>桌面資料庫驅動程式效能問題
若要確保現有的 ANSI 應用程式相容性，SQL_WCHAR、 SQL_WVARCHAR 和 SQL_WLONGVARCHAR 資料類型都會公開為 SQL_CHAR、 SQL_VARCHAR 和 SQL_LONGVARCHAR Microsoft 存取 4.0 或更高的資料來源。 資料來源不會傳回寬 CHAR 資料類型，但資料仍必須傳送至 Jet 寬字元格式。 請務必了解轉換過程可能需要的地方，是否 SQL_CHAR 資料型別 ANSI 應用程式中繫結 SQL_C_CHAR 參數或結果資料行。  
  
 類型 LONGVARCHAR 參數繫結 SQL_C_CHAR 類型時，這項轉換可以是就記憶體而言特別是效率不佳。 Jet 4.0 引擎是無法寫入資料流 LONGTEXT 參數資料，因為 UNICODE 轉換緩衝區必須配置兩次 ANSI SQL_C_CHAR 緩衝區的大小。 最有效率的機制是應用程式執行 UNICODE 轉換，並將參數繫結做為 SQL_C_WCHAR 類型。 當參數標示為執行資料，並會以 SQLPutData 的多個呼叫中提供的資料時，將長文字的資料緩衝區是而成長。 一種方式以避免這持續增加的費用 」 將資料 「 緩衝區是提供了選擇性的長度，透過 SQL_DATA_AT_EXEC_LEN(x)，其中*x*是預期的位元組長度。 這將會初始化內部 PutData 緩衝區的大小*x*位元組。  
  
> [!NOTE]  
>  插入或更新長資料的有效方式使用即可**SQLBulkOperations()** 或是**SQLSetPos()** 並將長資料設定為 SQL_DATA_AT_EXEC。 （EXEC_LEN 會忽略在此情況下。）可以在區塊串流資料，藉由呼叫**SQLPutData**多次，這會有效地將資料附加至資料表。  
  
 當應用程式使用 Microsoft ODBC 桌面資料庫驅動程式透過 Jet 3.5 資料庫升級為 4.0 版時，則可能會發生一些效能降低，而且增加的工作集大小。 這是因為當是第 3 版。*x*使用新的 4.0 版驅動程式來開啟資料庫，它會載入 Jet 4.0。 當開啟資料庫 Jet 4.0，並會看到，資料庫就會是 3。*x*版本，它會載入相當於載入 Jet 3.5 引擎也有可安裝的 ISAM 驅動程式。 若要移除的效能和大小負面影響，Jet 3。*x*應該到 Jet 4.0 格式資料庫壓縮資料庫。 這會消除載入兩個的 Jet 引擎，並最小化資料的程式碼路徑。  
  
 此外，Jet 4.0 引擎是 Unicode 引擎。 儲存所有字串，並且在 Unicode 中操作。 ANSI 應用程式存取 Jet 3 時。*x*為 Unicode，再回復成 ANSI，透過 Jet 4.0 引擎，資料的資料庫會從 ANSI 轉換。 如果資料庫更新至 4.0 版格式時，字串會轉換成 Unicode，移除一個層級的字串轉換，以及透過只有一個 Jet 引擎來減少資料的程式碼路徑中。
