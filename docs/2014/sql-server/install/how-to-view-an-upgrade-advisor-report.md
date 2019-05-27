---
title: HOW TO：檢視 Upgrade Advisor 報表 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- displaying reports
- viewing reports
- Upgrade Advisor [SQL Server], reports
- SQL Server Upgrade Advisor, reports
- reports [Upgrade Advisor], viewing
ms.assetid: d13b38af-0ac3-4030-83cd-e7d7825dd09f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c0ae231e380530f11d4c97a917927ed62e99fb47
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66094800"
---
# <a name="how-to-view-an-upgrade-advisor-report"></a>HOW TO：檢視 Upgrade Advisor 報表
  Upgrade Advisor 會針對您選取要分析的每個元件建立報表。 此主題描述如何從 Upgrade Advisor 開始頁面檢視 Upgrade Advisor 報表。  
  
> [!IMPORTANT]  
>  報表檢視器會根據標準檔案名稱載入檔案。 如果檔案已經重新命名，報表檢視器將不會載入它們。  
  
### <a name="to-view-a-report"></a>若要檢視報表  
  
1.  按一下 **開始**，按一下**所有程式**，按一下  **[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]**，然後按一下 **[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Upgrade Advisor**。  
  
2.  在 Upgrade Advisor 開始頁面上，按一下**啟動 Upgrade Advisor 報表檢視器**。  
  
3.  若要選取電腦上預設位置中的報表：  
  
    1.  在  **Server**清單中，選取伺服器。  
  
    2.  在 **執行個體或元件**清單中，選取的元件 / 執行個體的組合。  
  
     若要選取另一個位置的報表：  
  
    1.  按一下 **開啟報表**連結。  
  
    2.  瀏覽至報表位置，然後按兩下 XML 檔。  
  
     Upgrade Advisor 最多儲存先前分析的五個報表做為歷程記錄。 若要檢視這些報表，請按一下**報表**下拉式清單方塊中，然後選取報表。 這些報表是依其產生時的時間戳記列出。  
  
     報表包含所有已偵測之問題的下列詳細資料：  
  
    -   **重要性**，表示已修正此問題的重要性。  
  
    -   **修正**，這表示是否您應該 （或必須） 修正此問題之前或之後升級至[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 之前或之後移轉應用程式或資料，或任何時間。  
  
    -   問題的簡短描述。  
  
4.  如果報表包含超過 20 個項目，按一下報表頂端或底部的綠色前進箭頭，即可檢視下一組項目。 按一下綠色後退箭頭則可檢視前 20 個項目。  
  
5.  若要排序報表，請按一下資料行標題。  
  
6.  若要檢視特定項目的詳細資料，請按一下該項目。 問題的描述隨即顯示，並提供其他選項：  
  
    -   若要檢視的物件，其中找到此問題，請按一下**顯示受影響的物件**。  
  
    -   若要檢視問題的說明，請按一下**告訴我更多關於此問題，以及如何解決它**。  
  
    -   若要將標示為已解決，當您再次檢視報表時，會隱藏問題，問題選取**此問題已解決**。  
  
> [!NOTE]  
>  報表可能會包含無法偵測之問題的項目。 這些是無法偵測或是會產生過多誤判結果的問題。 按一下 **告訴我更多關於此問題，以及如何解決它**連結來查看元件無法偵測之問題的清單。  
  
## <a name="see-also"></a>另請參閱  
 [如何：將報表匯出](../../../2014/sql-server/install/how-to-export-reports.md)   
 [如何：執行 Upgrade Advisor 分析精靈](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [解決升級問題](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [Upgrade Advisor 的如何主題](../../../2014/sql-server/install/upgrade-advisor-how-to-topics.md)   
 [使用升級建議程式](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
