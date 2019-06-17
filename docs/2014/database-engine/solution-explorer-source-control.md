---
title: 方案總管原始檔控制 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Visual SourceSafe
- SQL Server Management Studio [SQL Server], source control services
- source-controlled files [SQL Server]
- source controls [SQL Server Management Studio], services
- version control services [SQL Server]
- file source control services [SQL Server]
- VSS [Visual SourceSafe]
ms.assetid: 6373adb8-3d81-4945-a9fc-1d0d5799d29a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 788ce615f914dcc8a2a49fba7575061fff0df870
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62843097"
---
# <a name="solution-explorer-source-control"></a>方案總管原始檔控制
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 方案總管可以整合到不同的原始檔控制系統中。 將方案或專案整合為原始檔控制系統之後，就可以控制專案中指令碼和查詢的檔案存取權和版本設定。  
  
## <a name="solution-and-project-source-control"></a>方案和專案原始檔控制  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../includes/ssnotedepfutureavoid-md.md)]  
  
 「原始檔控制」是指利用一段中央伺服器軟體來儲存和追蹤檔案版本及控制檔案存取動作的系統。 典型的原始檔控制系統包括一個原始檔控制提供者及兩個或更多原始檔控制用戶端。 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 可以與原始檔控制服務整合。 這表示此工具可用來做為您的原始檔控制提供者的用戶端。 在不離開環境的情況下，您很容易管理您的個別和團隊專案。 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 並未隨附原始檔控制提供者。  
  
#### <a name="to-select-a-source-control-provider"></a>若要選取原始檔控制提供者  
  
1.  安裝原始檔控制提供者的用戶端部份。  
  
2.  在 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]的 **[工具]** 功能表上，按一下 **[選項]** 。  
  
3.  在**選項**對話方塊方塊中，展開**原始檔控制**，然後按一下**外掛程式選取範圍**頁面。  
  
4.  在 **目前的原始檔控制外掛程式**方塊中，選取原始檔控制外掛程式。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[原始檔控制基本概念](../../2014/database-engine/source-control-basics.md)|定義基本的原始檔控制專有名詞，以及說明使用原始檔控制服務如何使專案受益。|  
|[將方案與專案新增原始檔控制](../../2014/database-engine/add-solutions-and-projects-to-source-control.md)|說明如何利用 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 環境，將方案和專案加入原始檔控制中。|  
|[從原始檔控制開啟方案和專案](../../2014/database-engine/open-solutions-and-projects-from-source-control.md)|說明如何利用 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 環境來開啟接受原始檔控制的方案和專案。|  
|[管理簽出](../../2014/database-engine/manage-checkouts.md)|說明如何從原始檔控制中簽出方案和檔案。|  
|[管理簽入](../../2014/database-engine/manage-checkins.md)|說明如何將方案和檔案簽入原始檔控制中。|  
|[設定及擷取版本資訊](../../2014/database-engine/set-and-retrieve-version-information.md)|說明如何擷取專案或項目的記錄、擷取項目的本機副本，或比較兩個項目版本。|  
|||  
  
## <a name="see-also"></a>另請參閱  
 [方案總管](../ssms/solution/solution-explorer.md)   
 [解決方案&#40;SQL Server Management Studio&#41;](../ssms/sql-server-management-studio-ssms.md)   
 [專案&#40;SQL Server Management Studio&#41;](../ssms/solution/projects-sql-server-management-studio.md)   
 [管理方案和專案的檔案](../ssms/solution/files-that-manage-solutions-and-projects.md)  
  
  
