---
title: SQL Server 監視器概觀 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.sqlservermonitor.main.f1
helpviewer_keywords:
- SQL Server Monitor [SQL Server]
ms.assetid: 048ae16d-31c3-489a-9f1e-1400a3bacd39
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 889e0c5a54477a1532aa9ec2760fad890a671618
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62755186"
---
# <a name="sql-server-monitor-overview"></a>SQL Server 監視器概觀
  「SQL Server 監視器」不會執行監視功能，但是它所主控的模組會執行該項功能。 「SQL Server 監視器」的模組包括「複寫監視器」和「資料庫鏡像監視器」。  
  
 若要使用其中一個模組，請在 **[執行]** 功能表上選取該模組。 目前選取的模組即擁有導覽窗格和詳細資料窗格的內容、使用者在詳細資料窗格中所做的動作，以及對內容和狀態的查詢。  
  
> [!NOTE]  
>  如需這些監視器的詳細資訊，請參閱 [監視複寫](../../relational-databases/replication/monitoring-replication.md) 和 [監視資料庫鏡像 &#40;SQL Server&#41;](../database-mirroring/database-mirroring-sql-server.md)。  
  
## <a name="permissions"></a>權限  
  
-   複寫監視器  
  
     若要監視複寫，您必須是「散發者」端 **sysadmin** 固定伺服器角色的成員，或是散發資料庫中 **replmonitor** 固定資料庫角色的成員。 系統管理員可以將任何使用者新增到 **replmonitor** 角色，此角色允許該使用者在「複寫監視器」中檢視複寫活動；不過，使用者不能管理複寫。  
  
-   資料庫鏡像監視器  
  
     若要監視資料庫鏡像，您必須是伺服器執行個體上 **sysadmin** 固定伺服器角色或 **dbm_monitor** 固定資料庫角色的成員。 如果您只是其中一個夥伴伺服器執行個體上 **系統管理員** 或 **dbm_monitor** 的成員，則監視器只能連接到該夥伴，不能從其他夥伴那裡擷取資訊。 如需詳細資訊，請參閱 [Database Mirroring Monitor Overview](../database-mirroring/database-mirroring-monitor-overview.md)。  
  
## <a name="menu-options"></a>功能表選項  
 「SQL Server 監視器」的功能表包含與「SQL Server 監視器」相關的命令。 這個功能表也可以包含選取之模組的命令。  
  
 下列是與「SQL Server 監視器」相關的功能表選項：  
  
 **檔案**  
 這個功能表包含 [結束]  命令。  
  
 **動作**  
 包含導覽樹狀目錄中選取之節點的內容功能表。  
  
 **Go**  
 包含監視元件的清單：  
  
-   資料庫鏡像  
  
-   複寫  
  
 **若要使用 SQL Server Management Studio 監視資料庫鏡像**  
  
-   [啟動資料庫鏡像監視器 &#40;SQL Server Management Studio&#41;](../database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="see-also"></a>另請參閱  
 [監視資料庫鏡像 &#40;SQL Server&#41;](../database-mirroring/database-mirroring-sql-server.md)  
  
  
