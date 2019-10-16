---
title: 比較和分析執行計劃 | Microsoft Docs
ms.custom: ''
ms.date: 11/21/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Showplan results
- execution plans [SQL Server]
- queries [SQL Server], tuning
- execution plans [SQL Server], how-to topics
- SQL Server Management Studio [SQL Server], execution plans
- tuning queries [SQL Server]
ms.assetid: bcd6f094-c613-4835-ae19-4caaadb4bb17
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 4b300d1fbc144f25b3f725f34e49d961953c434c
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/12/2019
ms.locfileid: "72289336"
---
# <a name="compare-and-analyze-execution-plans"></a>比較和分析執行計劃
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
本節會說明如何使用 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來比較和分析執行計劃。 從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] v17.4 開始提供此功能。  
  
執行計畫會以圖形化的方式，顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查詢最佳化工具所選擇的資料擷取方法。 執行計畫會使用圖示來呈現 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中特定陳述式與查詢的執行成本，而不是使用 [SET SHOWPLAN_ALL](../../t-sql/statements/set-showplan-all-transact-sql.md) 或 [SET SHOWPLAN_TEXT](../../t-sql/statements/set-showplan-text-transact-sql.md) 陳述式所產生的表格呈現方式。 這種圖形式的方法，對於了解查詢的效能特性非常有幫助。 

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 包含可讓使用者比較兩個執行計劃的功能，例如針對相同查詢比較被視為良好及不良的計劃，以及執行根本原因分析。 其中也包含了執行單一查詢計劃分析的功能，可讓您透過分析其執行計劃，來取得可能影響查詢效能案例的見解。

如需查詢執行計劃的詳細資訊，請參閱[估計執行計劃](../../relational-databases/performance/display-the-estimated-execution-plan.md)、[實際執行計劃](../../relational-databases/performance/display-an-actual-execution-plan.md)，以及[查詢處理架構指南](../../relational-databases/query-processing-architecture-guide.md)。
  
## <a name="in-this-section"></a>本節內容  
[比較執行計劃](../../relational-databases/performance/display-the-estimated-execution-plan.md)     
[分析實際執行計劃](../../relational-databases/performance/display-an-actual-execution-plan.md)      
  
