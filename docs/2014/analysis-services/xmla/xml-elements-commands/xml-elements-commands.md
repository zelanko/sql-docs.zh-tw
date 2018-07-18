---
title: 命令 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
- apinav
helpviewer_keywords:
- commands [XML for Analysis]
- XML for Analysis, commands
- XMLA, commands
ms.assetid: c8a93ea6-8eb5-4204-b037-69cb442a0082
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 215db39cdf87cff69f2bfefbc28e730590daec15
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37298888"
---
# <a name="commands-xmla"></a>命令 (XMLA)
  這個參考章節包含可在 `Command` 方法呼叫期間用於 `Execute` 元素中的 XML for Analysis (XMLA) 元素。  
  
|元素|描述|  
|-------------|-----------------|  
|[Alter 元素 (XMLA)](alter-element-xmla.md)|包含由所使用的 Analysis Services 指令碼語言 (ASSL) 元素[Execute](../xml-elements-methods-execute.md)方法來改變執行個體上的物件[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。|  
|[Backup 元素](backup-element-xmla.md)|備份[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]資料庫備份至備份檔案。|  
|[Batch 元素](batch-element-xmla.md)|執行一或多個 XML for Analysis (XMLA) 命令，以批次作業中，循序或平行執行個體上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。|  
|[BeginTransaction 元素](begintransaction-element-xmla.md)|在含有 Analysis Services 執行個體的目前工作階段上開始交易。|  
|[Cancel 元素](cancel-element-xmla.md)|取消 Analysis Services 執行個體上的目前執行中命令。|  
|[ClearCache 元素](clearcache-element-xmla.md)|針對 Analysis Services 執行個體上的指定物件清除記憶體快取。|  
|[CommitTransaction 元素](committransaction-element-xmla.md)|在含有 Analysis Services 執行個體的目前工作階段上認可交易。|  
|[Create 元素](create-element-xmla.md)|包含由所使用的 Analysis Services 指令碼語言 (ASSL) 元素[Execute](../xml-elements-methods-execute.md) Analysis Services 執行個體上建立物件的方法。|  
|[Delete 元素](delete-element-xmla.md)|刪除 Analysis Services 執行個體上的物件。|  
|[DesignAggregations 元素](designaggregations-element-xmla.md)|針對 Analysis Services 執行個體的彙總設計建立彙總。|  
|[Drop 元素](drop-element-xmla.md)|從維度中刪除屬性成員。|  
|[Insert 元素](insert-element-xmla.md)|將屬性成員插入維度中。|  
|[Lock 元素](lock-element-xmla.md)|鎖定 Analysis Services 執行個體上的指定物件。|  
|[MergePartitions 元素](mergepartitions-element-xmla.md)|將一個或多個來源資料分割的資料合併至目標資料分割中，然後刪除來源資料分割。|  
|[NotifyTableChange 元素](notifytablechange-element-xmla.md)|通知 Analysis Services 執行個體，表示指定資料來源中的資料表已經變更。|  
|[Process 元素](process-element-xmla.md)|處理 Analysis Services 執行個體上的物件。|  
|[Restore 元素](restore-element-xmla.md)|從備份檔還原 Analysis Services 資料庫。|  
|[RollbackTransaction 元素](rollbacktransaction-element-xmla.md)|在含有 Analysis Services 執行個體的目前工作階段上回復交易。|  
|[Statement 元素](statement-element-xmla.md)|包含查詢或陳述式來傳送使用[Execute](../xml-elements-methods-execute.md) Analysis Services 執行個體的方法。|  
|[Subscribe 元素](subscribe-element-xmla.md)|訂閱追蹤並從 Analysis Services 執行個體傳回包含追蹤事件的資料列集。|  
|[Synchronize 元素](synchronize-element-xmla.md)|同步處理 Analysis Services 資料庫與另一個現有的資料庫。|  
|[Unlock 元素](unlock-element-xmla.md)|解除鎖定 Analysis Services 執行個體上的指定鎖定。|  
|[Update 元素](../xml-elements-commands/update-element-xmla.md)|更新維度中的屬性成員。|  
|[UpdateCells 元素](updatecells-element-xmla.md)|更新可寫入 Cube 中的資料格。|  
  
  
