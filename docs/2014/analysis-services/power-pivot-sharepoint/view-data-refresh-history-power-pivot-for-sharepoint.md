---
title: 檢視資料重新整理記錄 (PowerPivot for SharePoint) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- unattended data refresh [Analysis Services with SharePoint]
- data refresh history [Analysis Services with SharePoint]
- scheduled data refresh [Analysis Services with SharePoint]
- data refresh [Analysis Services with SharePoint]
ms.assetid: 4c8d8aa8-794d-4f72-ace3-78d0e688e1a5
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5ecca7d87492645502e122497cc66eb54f083097
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37267584"
---
# <a name="view-data-refresh-history-powerpivot-for-sharepoint"></a>檢視資料重新整理記錄 (PowerPivot for SharePoint)
  資料重新整理記錄是 Excel 活頁簿中 PowerPivot 資料之所有資料重新整理活動的記錄。 資料重新整理作業會依您提供的排程，在 SharePoint 伺服器陣列中 Analysis Services 伺服器執行個體上執行。 根據預設，資料重新整理記錄會保留一年。 但是，伺服器陣列管理員可以為使用量和事件記錄指定不同的保留原則，用來決定資料重新整理記錄的保存時間。  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 | SharePoint 2010  
  
 **本主題內容：**  
  
 [必要條件](#prereq)  
  
 [檢視個別活頁簿的資料重新整理記錄](#viewhistory)  
  
 [檢視所有活頁簿的資料重新整理記錄](#viewITOps)  
  
 [使用記錄資訊](#pageelements)  
  
##  <a name="prereq"></a> 必要條件  
 您必須擁有「參與」或以上的權限，才能檢視資料重新整理記錄。  
  
 您必須已在含 PowerPivot 資料的活頁簿上，啟用並排程資料重新整理。 如果未排程資料重新整理，就會看到 [排程定義] 頁面，而不是 [記錄資訊] 頁面。  
  
##  <a name="viewhistory"></a> 檢視個別活頁簿的資料重新整理記錄  
  
1.  在 SharePoint 網站上，開啟包含具有 PowerPivot 資料之 Excel 活頁簿的文件庫。  
  
     沒有任何視覺指標，可識別在 SharePoint 文件庫中的哪個活頁簿包含 PowerPivot 資料。 您必須事先知道哪個活頁簿包含可重新整理的 PowerPivot 資料。  
  
2.  選取該活頁簿，然後按一下出現在右邊的向下箭號。  
  
3.  選取 **[管理 PowerPivot 資料重新整理]**。  
  
 記錄頁面隨即出現，其中顯示目前 Excel 活頁簿中 PowerPivot 資料之所有重新整理活動的完整記錄。  
  
##  <a name="viewITOps"></a> 檢視所有活頁簿的資料重新整理記錄  
 伺服器陣列管理員和服務應用程式管理員可以使用管理中心的 PowerPivot 管理儀表板，取得完整的資料重新整理記錄檢視，以及所有 PowerPivot 活頁簿的狀態。 如需詳細資訊，請參閱 < [PowerPivot Management Dashboard and Usage Data](power-pivot-management-dashboard-and-usage-data.md)。  
  
##  <a name="pageelements"></a> 使用記錄資訊  
 [資料重新整理記錄] 頁面提供有關每項重新整理作業的詳細資訊。 您可以使用此頁面上的資訊，以確認是否已進行重新整理，或判斷作業失敗的原因。  
  
|項目|描述|  
|----------|-----------------|  
|名稱|指定含 PowerPivot 資料之 Excel 活頁簿的檔案名稱。|  
|目前狀態|值包括：[已排程]、[正在重新整理]、[成功] 或 [失敗]。<br /><br /> **已排程**：當您初次建立排程時會顯示此值。 資料重新整理執行過第一次後，就不會再出現此狀態訊息。<br /><br /> **正在重新整理** ：表示該資料重新整理在進行中。 要求是在程序佇列中，或正在伺服器上執行。<br /><br /> **成功** ：表示上次資料重新整理作業已完成，而且已將更新的活頁簿存回 SharePoint 文件庫中。<br /><br /> **失敗** ：表示上次資料重新整理作業並未成功。 已重新整理資料並未儲存。 活頁簿中所包含的資料與資料重新整理開始之前相同。|  
|上次成功重新整理|指定上次順利完成資料重新整理的日期。|  
|下次排程更新|指定下次排程要進行資料重新整理的日期。<br /><br /> [正在設定排程] 連結會跳至 [排程定義] 頁面。 如果您在活頁簿上擁有「參與」權限，您可以按一下連結以檢視及修改排程資訊，控制活頁簿中 PowerPivot 資料的自動資料重新整理。|  
|Started|在 [記錄詳細資料] 區段之中，[已啟動] 會指出實際的處理時間。 實際的處理時間可能與您的排程不同。 在伺服器上有足夠記憶體可用時，就會開始進行處理。 如果伺服器非常忙碌，可能會在您指定的開始時間之後數小時，才開始進行處理。|  
|已完成|在 [記錄詳細資料] 區段之中，[已完成] 會指出資料重新整理作業完成的時間。 日期和時間表示活頁簿存回文件庫時的時間。<br /><br /> 如果資料重新整理失敗，會有一則或多則錯誤訊息說明失敗的原因。 您可以展開每項記錄，以檢視詳細的狀態。 每個資料來源都會個別列出，旁邊會有成功或失敗訊息，說明資料重新整理未完成的原因。|  
|Time|提供從資料重新整理開始到完成的累計時間。|  
|[狀態]|提供重新整理作業成功或失敗的歷程記錄。|  
  
## <a name="see-also"></a>另請參閱  
 [設定使用量資料收集的&#40;PowerPivot for SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)   
 [排程資料重新整理&#40;PowerPivot for SharePoint&#41;](../schedule-a-data-refresh-powerpivot-for-sharepoint.md)   
 [PowerPivot 資料重新整理](power-pivot-data-refresh.md)  
  
  
