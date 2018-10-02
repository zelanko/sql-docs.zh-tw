---
title: 備份時刻表 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.SWB.POINTINTIMERESTORE.F1
- sql13.swb.backuptimeline.f1
helpviewer_keywords:
- Backup Timeline
ms.assetid: ae3565f2-ddb2-4469-a992-7531d4f9ebb8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d4f751ec11f66c3edfa61920d17394dd6237e560
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47850956"
---
# <a name="backup-timeline"></a>備份時刻表
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用 [備份時間表] 對話方塊，尋找及指定將資料庫還原至某個時間點的備份。 透過按一下 [還原資料庫] 窗格 ([一般] 頁面) 上的 [時間表] 上，即可存取 [備份時間表] 對話方塊。 這個對話方塊可讓您檢視資料庫上所執行之還原作業的時間軸。  
  
 Database Recovery Advisor 會確定只選取要還原到該時間點所需的備份。 這些選取的備份為您的還原作業構成了建議的還原計畫。 您應該只使用選取的備份。 如需資料庫復原建議程式的相關資訊，請參閱[還原和復原概觀 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)。  
  
## <a name="restore-to"></a>還原至  
 系統預設會選取 **[上次建立的備份]** 。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 會選取適當的備份以還原資料庫，而且會將資料庫還原至上次備份的時間點。 按一下 [特定的日期與時間] 手動設定日期與時間 (選取特定的時間點)。  
  
 **[特定的日期與時間]** 會允許您在選取的特定日期和時間停止還原。 此時間表顯示在所選取日期和時間的 24 小時內執行之備份作業的呈現。  
  
 **日期**  
 輸入日期，或從下拉式清單中選取日期。  
  
 **Time**  
 輸入或選取日期，以指定還原停止的特定時間點。  
  
 **時間表間隔**  
 顯示時間軸上可檢視的間隔類型選項。  
  
## <a name="timeline-and-legend"></a>時間表和圖例  
 使用時間表下方的捲軸，沿著時間表向前和向後移動游標。 按一下備份以將捲軸移至備份結尾。 將滑鼠停留在標記上方，以顯示提供所選取備份組詳細資訊的工具提示。 下列標記會在時間表上顯示備份資訊。  
  
 大三角形  
 代表資料庫上執行的完整備份，表示執行每個完整備份的特定時間點。  
  
 小三角形  
 代表資料庫上執行的差異備份，表示執行每個差異備份的特定時間點。  
  
 綠色陰影區域  
 表示交易記錄備份的涵蓋範圍。  
  
 紅線  
 只能放置在時間軸上可能還原的位置。 沿著時間表移動紅線，可調整 **[日期]** 和 **[時間]** 方塊中所顯示的日期和時間。  
  
## <a name="see-also"></a>另請參閱  
 [還原資料庫 &#40;一般頁面&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)  
  
  
