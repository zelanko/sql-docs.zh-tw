---
title: 在 DirectQuery 模式中測試模型 |Microsoft 文件
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ad7ff3ee1b3d3f9366a6dcab983ae70f9ea83c12
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="test-a-model-in-directquery-mode"></a>在 DirectQuery 模式中測試模型
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  從設計開始著手，在每個開發階段的 DirectQuery 模式中，檢閱測試表格式模型的選項。  
  
## <a name="test-in-excel"></a>在 Excel 中進行測試 
  
 在 SSDT 中設計模型時，您可以使用 [在 Excel 中進行分析] 功能針對記憶體內部的範例資料集或關聯式資料庫，測試您的模型化決策。  當您按一下 [在 Excel 中進行分析] 時，會開啟對話方塊讓您指定選項。
 
 ![在 Excel DirectQuery 選項中進行分析](../../analysis-services/tabular-models/media/analyze-in-excel-directquery-options.png)
 
 如果開啟了模型的 DirectQuery 模式，即可指定 DirectQuery 連接模式，在此有兩個選項︰
 - **範例資料檢視** ：使用此選項，任何 Excel 查詢都會導向至含有記憶體內部範例資料集的範例資料分割。 當您想要確定您在量值、導出資料行或資料列層級安全性的任何 DAX 公式會正確執行時，此選項會很有用。
 
 - **完整資料檢視** ：使用此選項，任何 Excel 查詢都會先傳送至 Analysis Services，再到關聯式資料庫。 其實，此選項能完全發揮 DirecQuery 模式的作用。
 
 ### <a name="other-clients"></a>其他用戶端
 當您使用 [在 Excel 中進行分析] 時，會建立 .odc 連接檔案。 您可以使用這個檔案的連接字串資訊，從其他用戶端應用程式連接到您的模型。 加入額外的參數 DataView=Sample，則指定用戶端應該連接到範例資料分割。  
  
## <a name="monitor-query-execution-on-backend-systems-using-xevents-or-sql-profiler"></a>使用 xEvents 或 SQL Profiler 監視後端系統上的查詢執行 
 啟動工作階段追蹤，並連接到 SQL Server 關聯式資料庫，以監視來自表格式模型的連接︰  
  
-   [使用 SQL Server 擴充事件監視 Analysis Services](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)  
  
-   [使用 SQL Server Profiler 監視 Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md)  
  
 如果使用的是 Oracle 或 Teradata，請使用這些系統的追蹤監視工具。  
  
  
