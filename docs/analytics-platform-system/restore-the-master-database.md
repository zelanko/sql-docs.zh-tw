---
title: "還原 Master 資料庫 (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7870021a-0d89-422e-b8ea-1cc95b45c139
caps.latest.revision: "11"
ms.openlocfilehash: b82ef65734b6953c085436d5322e7bf42ef979b4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="restore-the-master-database"></a>還原 Master 資料庫
**還原 Master**頁面的 SQL Server PDW 組態管理員可讓您從備份還原 master 資料庫。  
  
## <a name="before-you-begin"></a>開始之前  
  
> [!IMPORTANT]  
> 若要執行還原，SQL Server PDW 必須刪除目前的主要資料庫，其中包含使用者的安全性資訊和資料庫目錄。 建議您執行還原之前讓目前的主要資料庫的備份。  
  
## <a name="to-restore-the-master-database"></a>還原 master 資料庫  
  
1.  啟動 Configuration Manager。 如需詳細資訊，請參閱[啟動組態管理員 &#40;Analytics Platform System &#41;](launch-the-configuration-manager.md).  
  
2.  在左窗格的 Configuration Manager 中，按一下 **還原 Master**。  
  
3.  選取要還原的主要備份。  
  
4.  按一下 **[套用]**。  
  
5.  若要執行還原，SQL Server PDW 會關閉所有設備的服務，並中斷與所有使用者。 在還原完成之後，SQL Server PDW 會重新啟動的應用裝置的服務。  
  
![DWConfig 應用裝置 PDW 還原 master](./media/restore-the-master-database/SQL_Server_PDW_DWConfig_ApplPDWRestore.png "SQL_Server_PDW_DWConfig_ApplPDWRestore")  
  
