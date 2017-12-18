---
title: "SSMS 輸出視窗 | Microsoft Docs"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Output Window [SQL Server Management Studio]
- Activity Monitor [SQL Server Management Studio]
- Object Explorer [SQL Server Management Studio]
ms.assetid: a2ce1a07-b4e2-471c-87d2-b8de5e6c6864
caps.latest.revision: "1"
author: shueybubbles
ms.author: davidshi
manager: kenvh
ms.workload: Inactive
ms.openlocfilehash: 68fedd92d79f508e0b85f369019a886356ed8475
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="output-window-in-sql-server-management-studio"></a>SQL Server Management Studio 中的輸出視窗
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)] 您可以使用按鍵組合 Ctrl+Alt+O 從 [檢視] 功能表開啟輸出視窗。 有多個輸出通道可供使用。

下表提供每個輸出通道的相關訊息類型概觀。

|通路|Description|
|-----------|---------------|  
|**遙測**|遙測資料流的性質是 Microsoft 收集的[匿名功能使用方式資料](sql-server-management-studio-ssms.md)。 這些事件對於您自己保留 SSMS 使用方式的記錄而言很實用。 當 [輸出] 視窗開啟時，能夠協助您識別展開的物件總管節點，以及在 SSMS 工作階段中執行的命令。|
|**物件總管**|此通道會輸出 SQL 查詢的查詢文字，以及查詢在物件總管中展開節點所需的耗用時間。 每個查詢都會記錄「開始查詢」與「結束查詢」事件。 每個事件都有時間戳記，以及已與受查詢實體建立關聯的 URN。 [URN](https://technet.microsoft.com/library/microsoft.sqlserver.management.smo.urn(v=sql.90).aspx) 是指基礎 SQL 管理物件，由 XPath 樣式的階層組成。 例如，在 "MyServer" 伺服器的 "Db" 資料庫中，若資料表名為 "Table1"，URN 即為 "Server[@Name='MyServer']/Database[@Name='Db']/Table[/@Name='Table1']"。 在物件總管中展開一個節點可能會使用不同參數執行多個類似查詢。 「結束查詢」事件會包含查詢的耗用時間與 TSQL 文字。 如果物件總管展開特定節點會異常緩慢，這份查詢資料對伺服器效能分析而言就會很有用。 **注意** - 並不是每個在物件總管中的節點，都會在展開時提供此層級的查詢詳細資料。|
|**活動監視器**|當伺服器的[活動監視器開啟](https://docs.microsoft.com/en-us/sql/relational-databases/performance-monitor/activity-monitor)時，此通道即開始。 這個資料流包含事件，會在監視器因連線問題而暫停時，顯示其中各查詢、錯誤訊息及通知的一部份查詢文字和時間戳記。 若活動監視器似乎處於閒置狀態或無法更新，請檢查此輸出通道來取得詳細資訊。|





