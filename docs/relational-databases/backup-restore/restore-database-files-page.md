---
title: 還原資料庫 (檔案頁面) | Microsoft 文件
description: 在 SQL Server 中還原資料庫時，使用 [還原資料庫] 對話方塊的 [檔案] 頁面，以管理資料庫中要還原的特定檔案。
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.restoredb.files.f1
- sql13.swb.restoredb.files.f1 in the code
ms.assetid: 714c36ea-a9f9-43a4-99f9-a6f73d1baf8e
author: cawrites
ms.author: chadam
ms.openlocfilehash: d94a143eae321f7ea01f97a54b351d72f8142ad6
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/23/2020
ms.locfileid: "96129149"
---
# <a name="restore-database-files-page"></a>還原資料庫 (檔案頁面)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  使用 **[還原資料庫]** 對話方塊的 **[檔案]** 頁面，管理資料庫中已選擇要還原的特定檔案。  
  
## <a name="options"></a>選項。  
  
### <a name="restore-database-files-as"></a>將資料庫檔案還原為  
 用來指派和管理已還原之檔案的新檔案路徑。  
  
 **將所有檔案重新放置到資料夾**  
 重新放置還原的檔案。  
  
|選項|描述|  
|------------|-----------------|  
|**資料檔資料夾**|輸入或搜尋還原的資料檔應該重新放置到的目標資料檔資料夾名稱。|  
|**記錄檔資料夾**|輸入或搜尋還原的記錄檔應該重新放置到的目標記錄檔資料夾。|  
  
 **邏輯檔案名稱**  
 為每個要還原的資料庫檔案顯示一個資料列。  
  
 **檔案類型**  
 顯示檔案類型。  
  
 **原始檔案名稱**  
 顯示已還原之檔案的原始檔案路徑。  
  
 **還原成**  
 列出已還原的檔案另存的檔案名稱。 輸入或搜尋適當的檔案名稱。  
  
## <a name="see-also"></a>另請參閱  
 [還原資料庫 &#40;一般頁面&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)   
 [還原資料庫 &#40;選項頁面&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)   
 [RESTORE 引數 &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)   
 [定義磁帶機的邏輯備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
