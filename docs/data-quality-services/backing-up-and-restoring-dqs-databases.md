---
title: 備份與還原 DQS 資料庫 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: ''
ms.component: data-quality-services
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f3091f62-2234-4a80-a615-cf14c2a1da85
caps.latest.revision: ''
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8780d75251877b88586798987cbba2acb5fe6aae
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2018
---
# <a name="backing-up-and-restoring-dqs-databases"></a>備份及還原 DQS 資料庫
  此主題描述如何備份及還原 DQS 資料庫。  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 必要條件  
  
-   您必須知道或記得您在 DQS 伺服器安裝期間所提供之資料庫主要金鑰的密碼。  
  
-   請確定 DQS 中沒有任何執行中的活動或處理序。 這可以使用 **[活動監控]** 畫面加以確認。 如需有關在此畫面工作的詳細資訊，請參閱＜ [Monitor DQS Activities](../data-quality-services/monitor-dqs-activities.md)＞。  
  
-   確定沒有任何使用者登入 DQS 伺服器。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
  
-   您的 Windows 使用者帳戶必須是 SQL Server 執行個體上系統管理員 (sysadmin) 固定伺服器角色的成員，才能執行備份和還原作業。  
  
-   您必須擁有 DQS_MAIN 資料庫的 dqs_administrator 角色，才能在 DQS 中終止任何執行中的活動或停止任何執行中的處理序。  
  
##  <a name="BackupRestore"></a> 備份及還原 DQS 資料庫  
  
1.  啟動 Microsoft SQL Server Management Studio，並連接到適當的 SQL Server 執行個體。  
  
2.  在 [物件總管] 中，展開 **[資料庫]** 節點。  
  
3.  備份 DQS_STAGING_DATA 資料庫。 如需備份 SQL Server 資料庫的逐步指示，請參閱[建立完整資料庫備份 &#40;SQL Server&#41;](../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)。  
  
4.  備份 DQS_PROJECTS 資料庫。  
  
5.  備份 DQS_MAIN 資料庫。  
  
6.  中斷連接目前的 SQL Server 執行個體，並連接到您想要還原這些資料庫的 SQL Server 執行個體。  
  
7.  還原 DQS_MAIN 資料庫。 如需還原 SQL Server 資料庫的逐步指示，請參閱[使用 SSMS 還原資料庫備份](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)。  
  
8.  還原 DQS_PROJECTS 資料庫。  
  
9. 還原 DQS_STAGING_DATA 資料庫。  
  
10. 在 [物件總管] 中，以滑鼠右鍵按一下伺服器，然後按一下 **[新增查詢]**。  
  
11. 在 [查詢編輯器] 視窗中複製以下 SQL 陳述式，並使用您在 DQS 安裝期間為資料庫主要金鑰提供的密碼來取代 <密碼>*\<*：  
  
    ```  
    USE [DQS_MAIN]  
    GO  
    EXECUTE [internal_core].[RestoreDQDatabases] '<PASSWORD>'  
    GO  
  
    ```  
  
12. 按 F5 執行陳述式。 檢查 **[結果]** 窗格，確認陳述式是否皆已成功地執行。  
  
## <a name="see-also"></a>另請參閱  
 [管理 DQS 資料庫](../data-quality-services/manage-dqs-databases.md)  
  
  
