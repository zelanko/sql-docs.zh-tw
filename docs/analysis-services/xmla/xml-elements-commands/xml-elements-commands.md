---
title: "命令 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- commands [XML for Analysis]
- XML for Analysis, commands
- XMLA, commands
ms.assetid: c8a93ea6-8eb5-4204-b037-69cb442a0082
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 19644de3ba240e417faa3d787360686d7b5c835f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="xml-elements---commands"></a>XML 項目-命令
  這個參考章節包含的 XML for Analysis (XMLA) 元素，可用於**命令**項目期間**Execute**方法呼叫。  
  
|元素|Description|  
|-------------|-----------------|  
|[Alter 元素 (XMLA)](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)|包含所使用的 Analysis Services 指令碼語言 (ASSL) 元素[Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法來修改物件的執行個體上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。|  
|[Backup 元素](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)|備份[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]資料庫備份至備份檔案。|  
|[批次項目](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)|執行一或多個 XML for Analysis (XMLA) 命令，以批次作業，循序或平行的執行個體上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。|  
|[BeginTransaction 元素](../../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)|在含有 Analysis Services 執行個體的目前工作階段上開始交易。|  
|[Cancel 元素](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)|取消 Analysis Services 執行個體上的目前執行中命令。|  
|[ClearCache 元素](../../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md)|針對 Analysis Services 執行個體上的指定物件清除記憶體快取。|  
|[CommitTransaction 元素](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)|在含有 Analysis Services 執行個體的目前工作階段上認可交易。|  
|[建立項目](../../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)|包含所使用的 Analysis Services 指令碼語言 (ASSL) 元素[Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) Analysis Services 執行個體上建立物件的方法。|  
|[刪除項目](../../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md)|刪除 Analysis Services 執行個體上的物件。|  
|[DesignAggregations 元素](../../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md)|針對 Analysis Services 執行個體的彙總設計建立彙總。|  
|[Drop 元素](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)|從維度中刪除屬性成員。|  
|[插入項目](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)|將屬性成員插入維度中。|  
|[鎖定元素](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)|鎖定 Analysis Services 執行個體上的指定物件。|  
|[MergePartitions 元素](../../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md)|將一個或多個來源資料分割的資料合併至目標資料分割中，然後刪除來源資料分割。|  
|[NotifyTableChange 元素](../../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md)|通知 Analysis Services 執行個體，表示指定資料來源中的資料表已經變更。|  
|[Process 元素](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|處理 Analysis Services 執行個體上的物件。|  
|[Restore 元素](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|從備份檔還原 Analysis Services 資料庫。|  
|[RollbackTransaction 元素](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)|在含有 Analysis Services 執行個體的目前工作階段上回復交易。|  
|[陳述式項目](../../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)|包含查詢或陳述式傳送使用[Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) Analysis Services 執行個體的方法。|  
|[Subscribe 元素](../../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md)|訂閱追蹤並從 Analysis Services 執行個體傳回包含追蹤事件的資料列集。|  
|[同步處理項目](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)|同步處理 Analysis Services 資料庫與另一個現有的資料庫。|  
|[Unlock 元素](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)|解除鎖定 Analysis Services 執行個體上的指定鎖定。|  
|[更新項目](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)|更新維度中的屬性成員。|  
|[UpdateCells 元素](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)|更新可寫入 Cube 中的資料格。|  
  
  
