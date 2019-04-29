---
title: Upgrade Advisor 進度 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor [SQL Server], analysis progress status
- analyzing system [Upgrade Advisor], progress information
- SQL Server Upgrade Advisor, analysis progress status
- monitoring analysis progress
- progress information [Upgrade Advisor]
- status information [Upgrade Advisor]
ms.assetid: a9e3d1c8-d492-4beb-93c7-f1bc40d4a910
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f7efb9258203efcffeb98bf4404faee5f80aff9a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63016335"
---
# <a name="upgrade-advisor-progress"></a>Upgrade Advisor 進度
  Upgrade Advisor 分析會以專用分析器開始，以便針對您所選取每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件執行分析。 分析元件時，會回報進度**進度** 對話方塊。  
  
## <a name="options"></a>選項。  
 **動作**  
 指定選取要分析的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件。  
  
 **狀態**  
 顯示從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件進度介面傳回的狀態值。  
  
 **Message**  
 顯示從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 個別分析器傳回的錯誤、失敗或成功訊息。  
  
> [!NOTE]  
>  如果分析所需時間過長，您可以停止分析、結束 Upgrade Advisor 分析精靈，然後重新執行精靈。 若要縮短分析時間，請選取更少的元件進行掃描。  
  
 分析完成時，報表會寫入檔案中。 您可以檢視報表，依序按一下**啟動報表**以啟動報表檢視器，從這個頁面。 如果您想要稍後檢視報表，您可以開啟**Upgrade Advisor 報表檢視器**從 Upgrade Advisor 開始頁面。  
  
> [!NOTE]  
>  每次您分析伺服器時，系統會儲存先前的報表。 這些報表使用時間戳記做為檔案名稱進行儲存。 報表檢視器會顯示最近儲存的五個報表。  
  
## <a name="see-also"></a>另請參閱  
 [如何：啟動 Upgrade Advisor](../../../2014/sql-server/install/how-to-launch-upgrade-advisor.md)   
 [如何：執行 Upgrade Advisor 分析精靈](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [SQL Server 元件](../../../2014/sql-server/install/sql-server-components.md)   
 [Upgrade Advisor 使用者介面參考](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)   
 [使用升級建議程式](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
