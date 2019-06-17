---
title: 快照集選項屬性頁面 （報表管理員） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f6641f59-5267-4f57-8957-63b93d1a9679
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7a73f3be75a7f0cadf633943aeafffb7217d8e29
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66101154"
---
# <a name="snapshot-options-properties-page-report-manager"></a>快照集選項屬性頁面 (報表管理員)
  使用 [快照集選項] 屬性頁面可以排程要加入至報表記錄的報表快照集，以及設定報表記錄中儲存之報表快照集的數目限制。  
  
> [!NOTE]  
>  並非所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本都提供此功能。 如需的版本所支援的功能清單[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，請參閱 <<c2> [ 額外的資料庫服務](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md#Add_DBServices)。  
  
## <a name="navigation"></a>巡覽  
 您可以使用下列程序，在使用者介面 (UI) 中導覽至這個位置。  
  
### <a name="to-open-the-snapshot-options-properties-page-for-a-report"></a>若要開啟報表的快照集選項屬性頁面  
  
1.  開啟報表管理員，然後找出您想要設定報表快照集屬性的報表。  
  
2.  將滑鼠停留在該報表上，然後按一下下拉箭號。  
  
3.  在下拉式功能表中，按一下 **[管理]** 。 這樣就會開啟該報表的 [一般] 屬性頁面。  
  
4.  選取 **[快照集選項]** 索引標籤。  
  
## <a name="options"></a>選項  
 **允許手動建立報表記錄**  
 選取此核取方塊，即可視需要將快照集加入報表記錄中。 選取此核取方塊會使 **[新增快照集]** 按鈕出現在 [記錄] 頁面上。  
  
 **將所有報表執行快照集都儲存在報表記錄**  
 選取此核取方塊，將根據報表執行屬性所建立的報表快照集，複製到報表記錄。 可以將報表執行屬性設定為，從產生的快照集來執行報表。 設定此報表記錄屬性，就可以將所有長期產生的報表快照集複本，放入報表記錄中作為保存。  
  
 **使用下列排程將快照集加入至報表記錄**  
 選取此核取方塊，即可根據排程將快照集加入報表記錄中。 您可以建立專用於此目的的排程，或者當某個預先定義的共用排程包含您要的排程資訊，可以選擇預先定義的共用排程。  
  
 **選取要保留的快照集數目**  
 選取下列選項來控制報表記錄中保留的報表數目。 報表記錄設定可以隨每一個報表而改變。  
  
-   選取 **[使用預設值]** 即可保留預設值。 報表伺服器管理員控制報表記錄儲存的主要設定。 若您選擇此選項，則可由此主要設定中取得保留的快照集數目。  
  
-   選取 **[不限制報表記錄中的快照集數目]** ，即可保留所有的報表記錄快照集。 您必須手動刪除快照集以縮減報表記錄的大小。  
  
-   選取 **[限制報表記錄的副本]** ，即可保留固定的快照集數目。 當達到限制時，就會從報表記錄中移除較舊的複本，增加較新複本所需的空間。  
  
 報表記錄會儲存在報表伺服器資料庫中。 如果您有想要保留記錄的大型報表或許多報表，請考慮限制報表記錄的數量，以便協助管理報表伺服器資料庫的磁碟空間需求。  
  
 **Apply**  
 按一下即可儲存您的變更。  
  
## <a name="see-also"></a>另請參閱  
 [將快照集加入報表記錄 &#40;報表管理員&#41;](report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [報表管理員 &#40;SSRS 原生模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [建立、修改及刪除報表記錄中的快照集](report-server/create-modify-and-delete-snapshots-in-report-history.md)   
 [報表管理員 F1 說明](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
