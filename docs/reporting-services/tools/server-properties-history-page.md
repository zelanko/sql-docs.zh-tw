---
title: 伺服器屬性 (歷程記錄頁面) | Microsoft Docs
ms.date: 06/10/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: tools
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.serverproperties.history.f1
ms.assetid: be9d8018-a46f-4625-9ae1-138ebe6b38ba
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 498bc994828c4ed7089a4aa223659f70d1c612b5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47663892"
---
# <a name="server-properties-history-page"></a>伺服器多個屬性 (記錄頁面)
  使用 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 的這個 [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] 頁面，即可設定要保留之報表記錄副本數目的預設值。 預設值會提供建立所有報表之報表記錄限制的初始設定。 您可以針對個別報表更改這些設定。  
  
 報表記錄是報表快照集的集合，包括在建立快照集時對於報表而言是最新的報表資料和配置。 您可以使用報表記錄來保留某份報表在特定日期或時間的副本。 您可以針對在原生模式報表伺服器上或設定為 SharePoint 整合模式之報表伺服器上執行的個別報表，建立和管理報表記錄。  
  
 報表記錄快照集會儲存在報表伺服器資料庫中。 如果您保留無限數量的快照集，請務必定期檢查資料庫大小，以便確保它的成長速度不會過快或耗用過多磁碟空間。  
  
 若要開啟此頁面：
 1) 啟動 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。
 2) 連接到報表伺服器執行個體。
 3) 以滑鼠右鍵按一下報表伺服器名稱，然後選取 [屬性]。
 4) 按一下 **[記錄]** ，即可開啟此頁面。  
  
## <a name="options"></a>選項。  
 **不限制報表記錄中的快照集數目**  
 保留所有報表記錄快照集。 您必須手動刪除快照集以縮減報表記錄的大小。  
  
 **限制報表記錄的副本**  
 保留固定數目的報表記錄快照集。 當達到限制時，就會從報表記錄中移除較舊的複本，增加較新複本所需的空間。  
  
 如果稍後限制報表記錄，則當現有的報表記錄超過指定的限制時，報表伺服器會將現有的報表記錄縮減至低於新限制的量。 會先刪除最舊的報表快照集。 如果報表記錄為空白或在限制以下，則會加入新報表快照集。 如果達到限制，加入新報表快照集時會刪除最舊的快照集。  
  
## <a name="see-also"></a>另請參閱  
 [設定報表伺服器屬性 &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
 [連接至 Management Studio 中的報表伺服器](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Management Studio F1 說明中的報表伺服器](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)  
  
  
