---
title: SQL Operations Studio （預覽） SQL Server Profiler 擴充功能 |Microsoft Docs
description: SQL Operations Studio （預覽） 的 SQL Server Profiler 擴充功能
ms.custom: tools|sos
ms.date: 07/19/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 190d54a4525a476b2c42c22d447264a1d95e7bc4
ms.sourcegitcommit: 4b21840f20195d70f255465666f7b409ba839d18
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2018
ms.locfileid: "39147015"
---
# <a name="sql-server-profiler-extension"></a>SQL Server Profiler 擴充功能

使用 XEvents 建置延伸模組會提供類似於 SQL Server Management Studio (SSMS) Profiler，除了簡單 SQL Server 追蹤解決方案的 SQL Server Profiler。 SQL Server Profiler 是非常好用，而且最佳的預設值的最常見的追蹤設定。 UX 適合用於瀏覽事件，並檢視相關聯的 TRANSACT-SQL (T-SQL) 文字。 SQL Operations Studio 的 SQL Server Profiler 也假設美好的預設值，用來收集 T-SQL 執行活動，具有簡單易用的 ux。

**一般 SQL Profiler 的使用案例：**

- 逐步執行問題查詢來找出問題原因。
- 尋找和診斷執行速度很慢的查詢。
- 擷取造成問題的 TRANSACT-SQL 陳述式系列。
- 監視 SQL Server，來微調工作負載的效能。
- 將效能計數器相互關聯以診斷問題。


## <a name="install-the-sql-server-profiler-extension"></a>安裝 SQL Server Profiler 擴充功能

1. 若要開啟擴充管理員及存取可用的擴充功能，選取 [擴充功能] 圖示，或選取**檢視**功能表中的**擴充功能**。
2. 選取可用的擴充功能以檢視其詳細資料。

   ![程式碼剖析工具延伸模組管理員](media/extensions/sql-server-profiler-extension/profiler-extension.png)

1. 選取您想要的延伸模組並**安裝**它。
2. 選取**重新載入**以啟用該擴充功能 (只有第一次安裝擴充功能時需要)。

## <a name="start-profiler"></a>啟動 Profiler

1. 若要啟動 Profiler，首先請在 [伺服器] 索引標籤中的伺服器的連接。
2. 您建立連線之後，請輸入**Alt + P**啟動 Profiler。
3. 若要啟動 Profiler，請輸入**Alt + s。** 您現在可以開始看到擴充的事件。
    ![程式碼剖析工具延伸模組管理員](media/extensions/sql-server-profiler-extension/view-profiler.png)    
1. 若要停止 Profiler，請輸入**Alt + s。** 這個快速鍵會切換。

## <a name="next-steps"></a>後續步驟

若要深入了解 Profiler 和擴充的事件，請參閱[擴充事件](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)。





