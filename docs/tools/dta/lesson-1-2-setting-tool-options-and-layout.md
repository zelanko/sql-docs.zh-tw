---
title: 設定工具選項和配置 |Microsoft 文件
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: dta
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-query-tuning
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: 43e97ce0-97bc-4a27-9485-5bbeb7190b85
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 68a4c894fb4defe848b146c59b3ad159ac3da287
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/17/2018
---
# <a name="lesson-1-2---setting-tool-options-and-layout"></a>課程 1-2-設定工具選項和配置
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]您可以設定選項來設定 Database Engine Tuning Advisor 圖形化使用者介面 (GUI) 會顯示在啟動時，它會使用時，字型，並調整其他工具的功能支援使用它。 這一頁的練習可讓您熟悉您可以設定的選項及如何設定它們。  
  
### <a name="set-the-tool-options"></a>設定工具選項  
  
1.  啟動 Database Engine Tuning Advisor。 在 Windows [開始] 功能表上，依序指向 [所有程式]、[[!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]]、[效能工具]，然後按一下 [Database Engine Tuning Advisor]。  
  
2.  在 **[工具]** 功能表上，按一下 **[選項]**。  
  
3.  在 [選項] 對話方塊中，檢視下列選項：  
  
    -   展開 [啟動時] 清單來檢視 Database Engine Tuning Advisor 啟動時所能顯示的項目。 依預設，會選取 [顯示新的工作階段]。  
  
    -   按一下 [變更字型]，了解您在 [一般] 索引標籤上可以為資料庫和資料表清單選擇哪些字型。執行微調之後，Database Engine Tuning Advisor 的建議方格和報表也會使用這個選項所選擇的字型。 依預設，Database Engine Tuning Advisor 會使用系統字型。  
  
    -   [最近使用清單中的項目數目] 的設定範圍在 **1** 和 **10** 之間。 請在 [檔案] 功能表上，按一下 [最近使用的工作階段] 或 [最近使用的檔案] 來設定所顯示清單中的最大項目數。 依預設，這個選項會設為 **4**。  
  
    -   當核取 [記住上次的微調選項] 時，依預設，Database Engine Tuning Advisor 會利用上一個微調工作階段所指定的微調選項來處理下一個微調工作階段。 請清除這個核取方塊來使用 Database Engine Tuning Advisor 微調選項預設值。 依預設，會選取這個選項。  
  
    -   依預設，會核取 [永久刪除工作階段之前先詢問] 來避免意外刪除微調工作階段。  
  
    -   依預設，會核取 [停止工作階段分析之前先詢問]，以避免在 Database Engine Tuning Advisor 分析工作負載完成之前不慎停止微調工作階段。  
  
## <a name="next-lesson"></a>下一課  
[第 2 課： 使用 Database Engine Tuning Advisor](../../tools/dta/lesson-2-using-database-engine-tuning-advisor.md)  
  
  
  
