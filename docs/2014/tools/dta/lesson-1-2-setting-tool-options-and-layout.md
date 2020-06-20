---
title: 設定工具選項和版面配置 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: 43e97ce0-97bc-4a27-9485-5bbeb7190b85
author: stevestein
ms.author: sstein
ms.openlocfilehash: 36139b916442b2c0f616d52d2b06efdbda2cfe03
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85048340"
---
# <a name="setting-tool-options-and-layout"></a>設定工具選項和配置
  您可以設定一些選項來設定 Database Engine Tuning Advisor 圖形化使用者介面 (GUI) 在啟動時所顯示的項目、它使用的字型，以及其他工具功能，以便對您使用它的方式，提供最好的支援。 這一頁的練習可讓您熟悉您可以設定的選項及如何設定它們。  
  
### <a name="set-the-tool-options"></a>設定工具選項  
  
1.  啟動 Database Engine Tuning Advisor。 在 Windows [開始]**** 功能表上，依序指向 [所有程式]****、[[!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]]、[效能工具]****，然後按一下 [Database Engine Tuning Advisor]****。  
  
2.  在 **[工具]** 功能表上，按一下 **[選項]** 。  
  
3.  在 [選項]**** 對話方塊中，檢視下列選項：  
  
    -   展開 [啟動時]**** 清單來檢視 Database Engine Tuning Advisor 啟動時所能顯示的項目。 依預設，會選取 [顯示新的工作階段]****。  
  
    -   按一下 [**變更字型**]，以查看您可以在 [**一般**] 索引標籤上，為資料庫和資料表清單選擇哪些字型。您為此選項選擇的字型也會在執行微調之後，用於 Database Engine Tuning Advisor 建議方格和報表中。 依預設，Database Engine Tuning Advisor 會使用系統字型。  
  
    -   [最近使用清單中的項目數目]**** 的設定範圍在 **1** 和 **10** 之間。 請在 [檔案]**** 功能表上，按一下 [最近使用的工作階段]**** 或 [最近使用的檔案]**** 來設定所顯示清單中的最大項目數。 依預設，這個選項會設為 **4**。  
  
    -   當核取 [記住上次的微調選項]**** 時，依預設，Database Engine Tuning Advisor 會利用上一個微調工作階段所指定的微調選項來處理下一個微調工作階段。 請清除這個核取方塊來使用 Database Engine Tuning Advisor 微調選項預設值。 預設會選取這個選項。  
  
    -   依預設，會核取 [永久刪除工作階段之前先詢問]**** 來避免意外刪除微調工作階段。  
  
    -   依預設，會核取 [停止工作階段分析之前先詢問]****，以避免在 Database Engine Tuning Advisor 分析工作負載完成之前不慎停止微調工作階段。  
  
## <a name="next-lesson"></a>下一課  
 [第 2 課：使用 Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  
