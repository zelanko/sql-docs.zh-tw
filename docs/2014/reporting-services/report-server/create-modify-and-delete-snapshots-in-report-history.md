---
title: 建立、修改及刪除報表記錄中的快照集 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- snapshots [Reporting Services]
- report snapshots [Reporting Services]
ms.assetid: 5aebbbfa-a8db-462d-8ab9-746fad9525f0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ecddbed328d1625f525069fe3d502c3348eb065a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66103906"
---
# <a name="create-modify-and-delete-snapshots-in-report-history"></a>建立、修改及刪除報表記錄中的快照集
  報表記錄是報表快照集的集合。 您可以加入和刪除快照集，或修改影響報表記錄儲存區的屬性，來維護報表記錄。 您可以用手動方式或依據排程來建立報表記錄。  
  
 若要建立報表記錄，您的角色指派必須包括「管理報表記錄」工作。 若要檢視報表記錄，您的角色指派必須包括「檢視報表」工作。 有報表存取權的使用者，都可以使用報表記錄。 您無法選擇性地針對部分使用者啟用或停用報表記錄。  
  
 報表記錄中的快照集可以由建立的日期及時間加以識別。 日期及時間是以查詢的執行時間為準。  
  
## <a name="creating-snapshots-in-report-history"></a>在報表記錄中建立快照集  
 您可以用手動方式建立快照集，如果是可以自動執行的報表，就能夠依排定間隔建立快照集。 若要自動執行，報表必須使用預存認證，或完全不使用認證。 此外，若報表使用參數，您必須指定報表執行時使用的預設值。 您可以在報表的屬性頁面指定預存認證和參數值。 如需詳細資訊，請參閱[參數屬性頁面 &#40;報表管理員&#41;](../parameters-properties-page-report-manager.md)。  
  
 當您在建立報表快照集時，下列元素會和報表快照集一起儲存在報表伺服器資料庫中：  
  
-   結果集 (就是報表中的資料，透過在報表的 [資料來源] 屬性頁面所指定的認證擷取而來的)。  
  
-   基礎報表定義，當快照集建立時便存在的定義。 如果在快照集產生之後，對報表定義做修改，所做的變更不會反映在快照集內。  
  
-   用來取得或篩選結果集的參數值。  
  
-   內嵌來源，例如影像。 連結到報表的外部來源，不會和報表快照集儲存在一起。  
  
 建立報表記錄的方式以及可儲存的報表快照集數量，是由設定值所決定。  
  
 如果報表產生錯誤，就不會建立快照集。 產生警告的報表若可繼續執行，則可以用來產生快照集。  
  
## <a name="modifying-properties-and-deleting-report-history"></a>修改屬性與刪除報表記錄  
 一旦報表快照集已存在，便無法加以修改。 然而，您可以藉由修改屬性來刪除報表記錄。  
  
 以下為刪除報表記錄的方式：  
  
-   針對單一或群組，以手動的方式刪除快照集。  
  
     您可以從報表管理員的 [記錄] 頁面中刪除快照集。 導覽至報表，按一下 [記錄]，選取您要刪除的快照集旁邊的核取方塊，然後按一下 **[刪除]** 。  
  
-   降低報表記錄限制，以減少儲存的快照集數量。 報表記錄限制可以針對報表伺服器或特定的報表進行設定。 當限制降低時，系統會從記錄中刪除最舊的快照集。  
  
 您無法以大量作業的方式，刪除儲存在報表伺服器中的所有報表記錄。  
  
 刪除報表時，報表記錄也會一併刪除。 例如，若您刪除每月銷售額報表而以較新版本加以取代，則所有和該報表關聯的報表記錄也會遭到刪除。 然而，如果您移動報表，則所有報表記錄會隨著移動。  
  
## <a name="see-also"></a>另請參閱  
 [建立報表記錄 &#40;SharePoint 整合模式的 Reporting Services&#41;](create-report-history-reporting-services-in-sharepoint-integrated-mode.md)   
 [報表管理員 &#40;SSRS 原生模式&#41;](../report-manager-ssrs-native-mode.md)   
 [報表伺服器內容管理 &#40;SSRS 原生模式&#41;](report-server-content-management-ssrs-native-mode.md)   
 [將快照集加入報表記錄 &#40;報表管理員&#41;](add-a-snapshot-to-report-history-report-manager.md)   
 [限制報表記錄 &#40;報表管理員&#41;](../reports/limit-report-history-report-manager.md)  
  
  
