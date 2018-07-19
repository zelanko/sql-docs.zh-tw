---
title: 第 9 課︰管理備份組和檔案快照集備份 | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016
ms.assetid: 766a0846-db15-4346-b814-4049039bcbfc
caps.latest.revision: 10
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 32a5bad72add276eae015433f697cad01b8158c3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32941913"
---
# <a name="lesson-9-manage-backup-sets-and-file-snapshot-backups"></a>第 9 課︰管理備份組和檔案快照集備份
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
在這一課，您將會使用 [sp_delete_backup &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md) 系統預存程序來刪除備份組。 這個系統預存程序會刪除備份檔案以及與這個備份組相關聯的每個資料庫檔案上的檔案快照集。  
  
> [!NOTE]  
> 如果您只是刪除 Azure Blob 容器中的備份檔案來嘗試刪除備份組，則只會刪除備份檔案本身，相關聯的檔案快照集將會予以保留。 如果您發現自己處於這種情況，請使用 [sys.fn_db_backup_file_snapshots &#40;Transact-SQL&#41;](../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md) 系統函數來識別孤立檔案快照集 URL，以及使用 [sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md) 系統預存程序來刪除每個孤立檔案快照集。 如需詳細資訊，請參閱  [Azure 中資料庫檔案的檔案快照集備份](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)。  
  
若要刪除檔案快照集備份組，請遵循下列步驟：  
  
1.  連接到 SQL Server Management Studio。  
  
2.  開啟新的查詢視窗，並連接到您的 Azure 虛擬機器中資料庫引擎的 SQL Server 2016 執行個體 (或具有這個容器之讀取和寫入權限的任何 SQL Server 2016 執行個體)。  
  
3.  將下列 Transact-SQL 指令碼複製並貼入 [查詢] 視窗中。 選取您想要刪除的記錄備份與其相關聯的檔案快照集。 適當地修改儲存體帳戶名稱以及您在第 1 課中所指定容器的 URL，並提供記錄備份檔案名稱，然後執行此指令碼。  
  
    ```  
  
    sys.sp_delete_backup 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/tutorial-9164-20150726012420.bak';  
  
    ```  
  
4.  在物件總管中，連接到 Azure 儲存體。  
  
5.  依序展開 [容器] 以及您在第 1 課中建立的容器，然後確認步驟 3 中所使用的備份檔案不再出現於這個容器中 (必要時，請重新整理節點)。  
  
    ![Azure 容器，顯示記錄備份 Blob 的刪除](../relational-databases/media/c0070b08-4667-4db5-aaff-987a404ec934.JPG "Azure 容器，顯示記錄備份 Blob 的刪除")  
  
6.  將下列 Transact-SQL 指令碼複製並貼入查詢視窗中，然後執行此指令碼，確認已刪除兩個檔案快照集。  
  
    ```  
  
    -- verify that two file snapshots have been removed  
    SELECT * from sys.fn_db_backup_file_snapshots ('AdventureWorks2014');  
  
    ```  
  
    ![顯示 2 個檔案快照集遭刪除的結果窗格](../relational-databases/media/f3891361-dfb6-4f4d-a090-ebfeb977981e.JPG "顯示 2 個檔案快照集遭刪除的結果窗格")  
  
**教學課程結束**  
  
## <a name="see-also"></a>另請參閱  
[Azure 中資料庫檔案的檔案快照集備份](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)  
[sp_delete_backup &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)  
[sys.fn_db_backup_file_snapshots &#40;Transact-SQL&#41;](../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)  
[sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md)  
  
  
  

