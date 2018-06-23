---
title: 使用報表 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- displaying reports
- overriding reports
- Upgrade Advisor Report Viewer
- reports [Upgrade Advisor], about reports
- formatting reports
- resolved issues [Upgrade Advisor]
- distributing reports [Reporting Services]
- filtering reports [Reporting Services]
- removing report items
- viewing reports
- rerunning analysis
- information issues [Upgrade Advisor]
- deleting report items
- icons [Upgrade Advisor]
- Upgrade Advisor [SQL Server], reports
- sending reports
- blocking issues [Upgrade Advisor]
- sharing reports
- reports [Upgrade Advisor]
- SQL Server Upgrade Advisor, reports
- modifying reports
- distributing reports [Reporting Services], about report distribution
- warnings [Upgrade Advisor]
- analyzing system [Upgrade Advisor], reports
ms.assetid: 4a3cb94a-a7ac-4cec-94c7-db26fcf6d161
caps.latest.revision: 39
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d71bcb0f6c695f540f1d38b1418c2c3282afea58
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36023474"
---
# <a name="using-reports"></a>使用報表
  Upgrade Advisor 分析精靈會為伺服器上分析的每個元件和每個執行個體 (如有必要) 產生個別報表。 報表會提供影響升級之已知問題的詳細資料。 報表還會提供解決識別問題之資訊和建議動作的連結。  
  
> [!NOTE]  
>  如果 Upgrade Advisor 報表檢視器在預設報表目錄中找不到任何報表，您可以使用從不同的目錄載入報表**開啟報表**連結。  
  
## <a name="viewing-reports"></a>檢視報表  
 您可以使用 Upgrade Advisor 報表檢視器來檢視 Upgrade Advisor 報表。 若要檢視報表，Upgrade Advisor 開始頁面上，按一下**啟動 Upgrade Advisor 報表檢視器**。  
  
 當您載入伺服器的報表之後，就可以選取想要查看升級問題的元件。 您可以套用篩選器，從**篩選依據**方塊，請參閱下列：  
  
-   所有問題  
  
-   所有升級的問題  
  
-   升級前的問題  
  
-   所有移轉的問題  
  
-   已解決的問題  
  
-   未解決的問題  
  
 如果您的報表含有 20 個以上的問題，您可以按一下移動至下一頁或上一頁組問題**後 20**或**前 20**頂端或底部的問題清單。  
  
 您可以選取從報表，以便檢視最多五個儲存的報表**報表**下拉式清單方塊。 這些報表是依其產生時的時間戳記列出。  
  
## <a name="report-format"></a>報表格式  
 報表檢視器會在三個資料行中顯示報表問題。 每個問題都是可摺疊的，如此您就可以隱藏描述，而單獨檢視主要資訊。  
  
 第一個資料行是**重要性**資料行。 圖示會顯示帶有 X 的紅色圓形 (表示阻礙或重要問題)，或顯示帶有驚嘆號的黃色三角形 (表示「警告」和「資訊」問題)，藉以指出每個問題的重要性。 第二個資料行，**修正**，表示您必須解決此問題。 您可以排序任何報告**重要性**或**修正**資料行。 第三個資料行，**描述**，列出問題的標題。  
  
 您可以展開問題來顯示其他資訊、展開連結來顯示有關解決問題的詳細資訊，還可以展開連結來顯示問題詳細資料。 當您按一下連結以取得問題的詳細資訊時，即會顯示「說明」主題並提供問題的資訊以及解決問題的指示。 您已修正問題，或若要管理您的動作項目，您可以將問題標示為完成選取之後**這個問題已解決**核取方塊。 如果您想要從升級問題的清單中移除已解決的問題，請按一下**重新整理**。 此問題將不再顯示在您針對同一個元件執行 Upgrade Advisor 分析精靈或套用之前**已解決的問題**中篩選**篩選依據**選項。  
  
## <a name="report-files"></a>報表檔案  
 Upgrade Advisor 分析精靈會在我的文件中建立報表\\[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Upgrade Advisor\110\Reports 目錄，並建立每個伺服器針對您所分析的子目錄。 這些報表檔案是遵循特定命名慣例的 XML 檔案。 當您啟動 Upgrade Advisor 報表檢視器時，就會顯示預設目錄中的報表檔案。 如果您將報表檔案複製到這個資料夾中，它們必須遵守命名慣例，否則報表檢視器將不會自動顯示它們。  
  
 如果您想要與其他人共用這項資訊，可以將 XML 報表傳送給他們。 或者，如果您想要使用其他應用程式，就可以將報表匯出成逗號分隔值檔案，以便用來建立試算表、文字檔或電子郵件訊息。  
  
## <a name="see-also"></a>另請參閱  
 [如何： 檢視 Upgrade Advisor 報表](../../../2014/sql-server/install/how-to-view-an-upgrade-advisor-report.md)   
 [如何： 將報表匯出](../../../2014/sql-server/install/how-to-export-reports.md)   
 [如何： 篩選報表](../../../2014/sql-server/install/how-to-filter-reports.md)   
 [解決升級問題](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor&#91;新&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
