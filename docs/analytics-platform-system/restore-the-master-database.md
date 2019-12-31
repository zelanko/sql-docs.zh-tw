---
title: 還原 master 資料庫
description: 在 Analytics Platform System （AP）中還原 master 資料庫。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6d122881f5283da86f66494ee2f049756d151551
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400457"
---
# <a name="restore-the-master-database-in-analytics-platform-system-aps"></a>在 Analytics Platform System （AP）中還原 master 資料庫
SQL Server PDW Configuration Manager 的 [**還原主版**] 頁面可讓您從備份還原 master 資料庫。  
  
## <a name="before-you-begin"></a>開始之前  
  
> [!IMPORTANT]  
> 若要執行還原，SQL Server PDW 必須刪除目前的 master 資料庫，其中包含使用者安全性資訊和資料庫目錄。 建議您在執行還原之前，先備份目前的 master 資料庫。  
  
## <a name="to-restore-the-master-database"></a>還原 master 資料庫  
  
1.  啟動 Configuration Manager。 如需詳細資訊，請參閱[&#40;分析平臺系統&#41;啟動 Configuration Manager ](launch-the-configuration-manager.md)。  
  
2.  在 Configuration Manager 的左窗格中，按一下 [**還原主要**]。  
  
3.  選取要還原的主要備份。  
  
4.  按一下 **[套用]**。  
  
5.  若要執行還原，SQL Server PDW 將會關閉所有設備服務，並中斷所有使用者的連線。 還原完成之後，SQL Server PDW 會重新開機設備服務。  
  
![DWConfig 應用裝置 PDW 還原 master](./media/restore-the-master-database/SQL_Server_PDW_DWConfig_ApplPDWRestore.png "SQL_Server_PDW_DWConfig_ApplPDWRestore")  
  
