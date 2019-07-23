---
title: 壓縮資料庫工作 (維護計畫) | Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- Shrink Database Task
- Shrink Database(s) Task
- sql13.swb.maint.shrink.f1
helpviewer_keywords:
- Shrink Database Task dialog box
ms.assetid: a9874cac-cded-4145-9c38-8aafd267dbee
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: bbba27f582b65fdcc99ed8fda4d892b9a92eebb6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68115562"
---
# <a name="shrink-database-task-maintenance-plan"></a>壓縮資料庫工作 (維護計畫)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用 [壓縮資料庫工作]  對話方塊來建立嘗試縮減選取之資料庫大小的工作。 使用下列選項以決定將資料庫縮小之後，要在資料庫中保留的未使用空間數量 (百分比愈大，資料庫可縮小的程度愈小)。 這個值是根據資料庫中實際資料的百分比而取得。 例如：一個 100 MB 的資料庫，包含 60 MB 的資料及 40 MB 的可用空間，設定可用空間的百分比為 50 時，則結果為 60 MB 的資料及 30 MB 的可用空間 (因為 60 MB 的百分之 50 為 30 MB)。 只有資料庫中超出的空間會被刪除。 有效的數值範圍為 0 到 100。  
  
 將資料頁面從檔案結尾移到靠近檔案前端的未使用空間，以壓縮資料並復原儲存空間。 當檔案結尾建立了足夠的可用空間後，檔案結尾的資料頁面便可取消配置並返回檔案系統。  
  
> [!WARNING]  
>  為壓縮檔案所移動的資料可散佈至檔案中的任何可用位置。 如此會造成索引片段，並可能導致大範圍之索引搜尋的查詢效能變慢。 若要消除資料片段，可考慮在壓縮之後重建該檔案的索引。  
  
 此工作會執行 DBCC SHRINKDATABASE 陳述式。  
  
## <a name="options"></a>選項  
 **[連接]**  
 選取執行此工作時要使用的伺服器連接。  
  
 **新增**  
 建立新的伺服器連接，以便執行此工作時使用。 下面會描述 **[新增連接]** 對話方塊。  
  
 **資料庫**  
 指定受此工作影響的資料庫。  
  
-   **所有資料庫**  
  
     產生維護計畫，針對所有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫執行維護工作，但 tempdb 除外。  
  
-   **所有系統資料庫**  
  
     產生維護計畫，針對每個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料庫執行維護工作，但 tempdb 除外。 不會針對使用者建立的資料庫執行維護工作。  
  
-   **所有使用者資料庫**  
  
     產生維護計畫，針對所有使用者建立的資料庫執行維護工作。 不會對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料庫執行任何維護工作。  
  
-   **下列資料庫**  
  
     產生維護計畫，只針對選取的資料庫執行維護工作。 如果選擇此選項，則必須在清單中至少選取一個資料庫。  
  
    > [!NOTE]  
    >  維護計畫只針對相容性層級設為 80 (含) 以上的資料庫來執行。 不會顯示相容性層級設為 70 或更低的資料庫。  
  
 **壓縮資料庫當它超過**  
 指定使工作執行的大小 (MB)。  
  
 **壓縮後要保持的可用空間量**  
 當資料庫檔案中的可用空間達到此大小時停止壓縮。  
  
 **檢視 T-SQL**  
 根據選取的選項，檢視此工作在伺服器上執行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
> [!NOTE]  
>  受影響的物件數目較為大量時，會多花一些時間才會顯示。  
  
## <a name="new-connection-dialog-box"></a>新增連接對話方塊  
 **連接名稱**  
 輸入新連接的名稱。  
  
 **選取或輸入伺服器名稱**  
 選取執行此工作時要連接的伺服器。  
  
 **[重新整理]**  
 重新整理可用的伺服器清單。  
  
 **輸入要登入到伺服器的資訊**  
 指定如何對伺服器進行驗證。  
  
 **使用 Windows NT 整合式安全性**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 的執行個體。  
  
 **使用特定的使用者名稱和密碼**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 無法使用此選項。  
  
 **User name**  
 提供驗證時要使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。 無法使用此選項。  
  
 **密碼**  
 提供驗證時要使用的密碼。 無法使用此選項。  
  
## <a name="see-also"></a>另請參閱  
 [DBCC SHRINKDATABASE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)  
  
  
