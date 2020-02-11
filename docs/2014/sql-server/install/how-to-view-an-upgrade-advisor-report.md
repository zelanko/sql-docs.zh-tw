---
title: 如何：查看 Upgrade Advisor 報表 |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66094800"
---
# <a name="how-to-view-an-upgrade-advisor-report"></a>如何：檢視 Upgrade Advisor 報表
  Upgrade Advisor 會針對您選取要分析的每個元件建立報表。 此主題描述如何從 Upgrade Advisor 開始頁面檢視 Upgrade Advisor 報表。  
  
> [!IMPORTANT]  
>  報表檢視器會根據標準檔案名稱載入檔案。 如果檔案已經重新命名，報表檢視器將不會載入它們。  
  
### <a name="to-view-a-report"></a>若要檢視報表  
  
1.  依序按一下 [**開始**]、[ **[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]****所有程式**]、[]，然後按一下** [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [Upgrade Advisor**]。  
  
2.  在 Upgrade Advisor 開始頁面上，按一下 [**啟動 Upgrade Advisor 報表檢視器]**。  
  
3.  若要選取電腦上預設位置中的報表：  
  
    1.  在 [**伺服器**] 清單中，選取伺服器。  
  
    2.  在 [**實例或元件**] 清單中，選取 [元件] 或 [元件/實例] 組合。  
  
     若要選取另一個位置的報表：  
  
    1.  按一下 [**開啟報表**] 連結。  
  
    2.  瀏覽至報表位置，然後按兩下 XML 檔。  
  
     Upgrade Advisor 最多儲存先前分析的五個報表做為歷程記錄。 若要查看這些報表，請按一下 [**報表**] 下拉式清單方塊，然後選取報表。 這些報表是依其產生時的時間戳記列出。  
  
     報表包含所有已偵測之問題的下列詳細資料：  
  
    -   [**重要性**]，表示修正問題的重要程度。  
  
    -   **修正**時機，這表示您應該（或必須）在升級至[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]之前或之後，或在遷移應用程式或資料之前或之後，或在任何時間之前，修正此問題。  
  
    -   問題的簡短描述。  
  
4.  如果報表包含超過 20 個項目，按一下報表頂端或底部的綠色前進箭頭，即可檢視下一組項目。 按一下綠色後退箭頭則可檢視前 20 個項目。  
  
5.  若要排序報表，請按一下資料行標題。  
  
6.  若要檢視特定項目的詳細資料，請按一下該項目。 問題的描述隨即顯示，並提供其他選項：  
  
    -   若要查看找到這個問題的物件，請按一下 [**顯示受影響的物件**]。  
  
    -   若要查看問題的說明，請按一下 [**告訴我有關此問題的詳細資訊] 和 [解決方法**]。  
  
    -   若要將問題標示為已解決，這會在您再次查看報表時隱藏問題，請選取 [**此問題已解決**]。  
  
> [!NOTE]  
>  報表可能會包含無法偵測之問題的項目。 這些是無法偵測或是會產生過多誤判結果的問題。 按一下 [**告訴我有關此問題的詳細資訊] 和 [如何解決它**] 連結，以查看元件的無法偵測問題清單。  
  
## <a name="see-also"></a>另請參閱  
 [如何：匯出報表](../../../2014/sql-server/install/how-to-export-reports.md)   
 [如何：執行 Upgrade Advisor 分析嚮導](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [解決升級問題](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [Upgrade Advisor 的 how to 主題](../../../2014/sql-server/install/upgrade-advisor-how-to-topics.md)   
 [使用 Upgrade Advisor](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
