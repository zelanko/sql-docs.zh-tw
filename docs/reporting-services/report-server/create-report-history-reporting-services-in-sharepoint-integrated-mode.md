---
title: 建立報表記錄 (SharePoint 整合模式的 Reporting Services) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- report history [Reporting Services], SharePoint
ms.assetid: e57ec746-05ae-4ff6-8e39-6cde87310daa
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4034d7a2892ede43f364d0ebdd105314b6107ff2
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "65580360"
---
# <a name="create-report-history-reporting-services-in-sharepoint-integrated-mode"></a>建立報表記錄 (SharePoint 整合模式的 Reporting Services)
  報表記錄是您在經過一段時間後建立之報表快照集的集合。 每個快照集都是報表的副本，因為它在報表建立時就存在了。 它包含了快照集建立時報表最新的配置和資料。 轉譯資訊不會與快照集一起儲存。 當您在報表記錄中開啟快照集時，它就會以 HTML 在報表檢視器 Web 組件中開啟。 轉譯完成之後，您可以將它匯出成其他的應用程式格式。  
  
 若要建立報表記錄，報表必須能夠自動執行 (亦即，報表伺服器必須能夠在使用者不介入的情況下執行)。 您必須在包含報表的文件庫上擁有「編輯項目」權限。 若要檢視或刪除報表記錄，則必須擁有「檢視版本」或「刪除版本」的權限。  
  
### <a name="to-create-a-snapshot-or-report-history-on-demand"></a>若要視需要建立快照集或報表記錄  
  
1.  指向報表。  
  
2.  按一下以顯示向下箭頭，然後選取 [檢視報表記錄]  。  
  
3.  按一下 **[新增快照集]** 。 如果沒有顯示此按鈕，就是因為您沒有在報表記錄中建立快照集的權限。  
  
4.  若要檢視您剛建立的快照集，請從清單中選取它。 每個快照集都可由快照集建立時顯示的時間戳記加以識別。 您不能重新命名、移動或修改快照集。  
  
### <a name="to-schedule-report-history"></a>排程報表記錄  
  
1.  指向報表。  
  
2.  按一下以顯示向下箭頭，然後選取 [管理處理選項]  。  
  
3.  在 [記錄快照集選項]  中，按一下 [在排程上建立報表記錄快照集]  。  
  
4.  如果您設有包含想要使用之排程資訊的共用排程，請按一下 [在共用排程上]  ，然後選取想要使用的排程。 否則，請按一下 [在自訂排程上]  ，然後按一下 [設定]  指定依據重複執行排程建立報表記錄的選項。  
  
### <a name="to-create-report-history-when-data-is-refreshed-in-a-report"></a>在報表中的資料重新整理時建立報表記錄  
  
1.  指向報表。  
  
2.  按一下以顯示向下箭頭，然後選取 [管理處理選項]  。  
  
3.  在 [記錄快照集選項]  中，按一下 [在報表記錄中儲存所有報表資料快照集]  。  
  
## <a name="see-also"></a>另請參閱  
 [設定處理選項 &#40;SharePoint 整合模式的 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)  
  
  
