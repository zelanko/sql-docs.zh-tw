---
title: 還原 master 資料庫-Analytics Platform System |Microsoft Docs
description: 還原 master 資料庫中分析平台系統。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 184184f332225e76e152c2d909cfff788b4fea91
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62678434"
---
# <a name="restore-the-master-database-in-analytics-platform-system"></a>還原 master 資料庫中 Analytics Platform System
**還原 Master**頁面的 SQL Server PDW 組態管理員可讓您從備份還原 master 資料庫。  
  
## <a name="before-you-begin"></a>開始之前  
  
> [!IMPORTANT]  
> 若要執行還原，SQL Server PDW 必須刪除目前的主要資料庫，其中包含使用者的安全性資訊和資料庫目錄。 建議您讓目前的主要資料庫的備份，然後執行還原。  
  
## <a name="to-restore-the-master-database"></a>還原 master 資料庫  
  
1.  啟動組態管理員。 如需詳細資訊，請參閱 <<c0> [ 啟動組態管理員 &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)。</c0>  
  
2.  在左窗格的 Configuration Manager 中，按一下**還原 Master**。  
  
3.  選取要還原的主要備份。  
  
4.  按一下 **[套用]**。  
  
5.  若要執行還原，SQL Server PDW 將關閉所有設備的服務，並中斷與所有使用者。 在還原完成之後，SQL Server PDW 會重新啟動的設備服務。  
  
![DWConfig 應用裝置 PDW 還原 master](./media/restore-the-master-database/SQL_Server_PDW_DWConfig_ApplPDWRestore.png "SQL_Server_PDW_DWConfig_ApplPDWRestore")  
  
