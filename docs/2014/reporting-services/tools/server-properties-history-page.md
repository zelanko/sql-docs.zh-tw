---
title: 伺服器屬性 (歷程記錄頁面) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.serverproperties.history.f1
ms.assetid: be9d8018-a46f-4625-9ae1-138ebe6b38ba
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5ce48c964ec756668aa12566c494d9ae9a1e5372
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66099580"
---
# <a name="server-properties-history-page"></a>伺服器多個屬性 (記錄頁面)
  使用此頁面，即可設定要保留之報表記錄副本數目的預設值。 預設值會提供建立所有報表之報表記錄限制的初始設定。 您可以針對個別報表更改這些設定。  
  
 報表記錄是報表快照集的集合，包括在建立快照集時對於報表而言是最新的報表資料和配置。 您可以使用報表記錄來保留某份報表在特定日期或時間的副本。 您可以針對在原生模式報表伺服器上或設定為 SharePoint 整合模式之報表伺服器上執行的個別報表，建立和管理報表記錄。  
  
 報表記錄快照集會儲存在報表伺服器資料庫中。 如果您保留無限數量的快照集，請務必定期檢查資料庫大小，以便確保它的成長速度不會過快或耗用過多磁碟空間。  
  
 若要開啟此頁面，請啟動 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、連接至報表伺服器執行個體、以滑鼠右鍵按一下報表伺服器名稱，然後選取 [屬性]****。 按一下 **[記錄]** ，即可開啟此頁面。  
  
## <a name="options"></a>選項。  
 **不限制報表記錄中的快照集數目**  
 保留所有報表記錄快照集。 您必須手動刪除快照集以縮減報表記錄的大小。  
  
 **限制報表記錄的副本**  
 保留固定數目的報表記錄快照集。 當達到限制時，就會從報表記錄中移除較舊的複本，增加較新複本所需的空間。  
  
 如果稍後限制報表記錄，則當現有的報表記錄超過指定的限制時，報表伺服器會將現有的報表記錄縮減至低於新限制的量。 會先刪除最舊的報表快照集。 如果報表記錄為空白或在限制以下，則會加入新報表快照集。 如果達到限制，加入新報表快照集時會刪除最舊的快照集。  
  
## <a name="see-also"></a>另請參閱  
 [將報表伺服器屬性設定 &#40;Management Studio&#41;](set-report-server-properties-management-studio.md)   
 [連接到 Management Studio 中的報表伺服器](connect-to-a-report-server-in-management-studio.md)   
 [Management Studio F1 說明中的報表伺服器](report-server-in-management-studio-f1-help.md)  
  
  
