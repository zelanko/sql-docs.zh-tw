---
title: 分析實際執行計劃 | Microsoft Docs
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- analyzing execution plans
- analyzing actual execution plans
- execution plans [SQL Server], analyzing
ms.assetid: 9e583a18-5f4a-4054-bfe1-4b2a76630db6
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 089cc2fd9a2131ab18fea01262f9bc0d476355e4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773140"
---
# <a name="analyze-an-actual-execution-plan"></a>分析實際執行計劃

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

此主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 計劃分析功能來分析實際圖形化執行計劃。 從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] v17.4 開始提供此功能。 我們一般建議您[安裝最新版的 SSMS](../../ssms/download-sql-server-management-studio-ssms.md)。

> [!NOTE]
> 實際執行計畫是在執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢或 Batch 後產生。 基於這個緣故，實際執行計劃包含執行階段資訊；例如，實際資料列數目、資源使用量計量和執行階段警告 (如果有的話)。 如需詳細資訊，請參閱[顯示實際執行計劃](../../relational-databases/performance/display-an-actual-execution-plan.md)。
  
查詢效能的疑難排解需要在了解查詢處理和執行計劃方面具有大量的專業知識，才能夠實際找出並修正根本原因。

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 包含可在實際執行計劃分析的工作中實作某種程度的自動化功能，特別是針對大型且複雜的計劃。 目標是更輕鬆地找到不正確的[基數估計](../../relational-databases/performance/cardinality-estimation-sql-server.md)案例，並取得提供可能防護方法的建議。

> [!IMPORTANT]
> 請確定在將防護方法套用至生產環境之前，將對所建議防護方法進行適當的測試。
  
## <a name="to-analyze-an-execution-plan-for-a-query"></a>分析查詢的執行計劃  
  
1.  使用 [檔案]  功能表並按一下 [開啟檔案]  來開啟先前已儲存的查詢執行計劃檔案 (.sqlplan)，或將計劃檔案拖曳至 [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] 視窗。 或者，如果您只執行查詢並選擇顯示它的執行計劃，請移至結果窗格中的 [執行計劃]  索引標籤。 

2.  以滑鼠右鍵按一下執行計劃的空白區域，然後按一下 [分析實際執行計劃]  。 

    ![以滑鼠右鍵按一下 [分析實際執行計畫]](../../relational-databases/performance/media/plananalysismenuoption.png "以滑鼠右鍵按一下 [分析實際執行計畫]")   

3.  [執行程序表分析]  視窗隨即在底部開啟。 使用多個陳述式來分析計劃時，藉由使用正確的陳述式進行分析，[多個陳述式]  索引標籤非常實用。

4.  選取 [案例] 索引標籤，以查看實際執行計劃中所發現問題的詳細資料。 針對左窗格上每個列出的運算子，右窗格會在 [按一下這裡可取得此案例的詳細資訊]  連結中顯示有關案例的詳細資料，並列出可能原因來說明該案例。

    ![執行計畫分析結果](../../relational-databases/performance/media/plananalysis-scenarios.png "執行計畫分析結果") 
