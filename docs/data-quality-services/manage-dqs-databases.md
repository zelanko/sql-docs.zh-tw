---
title: "管理 DQS 資料庫 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: 
ms.component: data-quality-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 655a67aa-d662-42f2-b982-c6217125ada8
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 52b592c3f44f64601101cc603e2205c53a56180f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="manage-dqs-databases"></a>管理 DQS 資料庫
  本節針對 DQS 資料庫提供可執行之資料庫管理活動的相關資訊，如備份/還原或卸離/附加等。  
  
##  <a name="BackupRestore"></a> 備份與還原 DQS 資料庫  
 備份和還原 SQL Server 資料庫是資料庫管理員經常執行的作業，可在發生嚴重損毀時復原備份資料庫中的資料來避免資料遺失。 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 主要是由兩個 SQL Server 資料庫所實作：DQS_MAIN 和 DQS_PROJECTS。 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 資料庫的備份與還原程序類似於其他任何 SQL Server 資料庫。在備份和還原 DQS 資料庫時，要面臨三個挑戰：  
  
-   DQS 資料庫的備份和還原作業必須同步處理。 否則，還原的 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 將無法運作。  
  
-   兩個 DQS 資料庫 DQS_MAIN 和 DQS_PROJECTS 除了簡單資料庫物件 (例如資料表和預存程序) 以外，也包含組件與其他複雜物件。  
  
-   DQS 資料庫之外必須有一些實體存在，DQS 資料庫才能當做 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]運作，特別是兩個 SQL Server 登入 (##MS_dqs_db_owner_login## 和 ##MS_dqs_service_login##) 及 master 資料庫中的初始化預存程序 (DQInitDQS_MAIN)。  
  
 如需有關 SQL Server 中之備份與還原的詳細資訊，請參閱＜ [SQL Server 資料庫的備份與還原](../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)＞。  
  
### <a name="default-autogrowth-size-and-recovery-model-for-the-dqs-databases"></a>DQS 資料庫的預設自動成長大小和復原模式  
 為了避免 DQS 資料庫和交易記錄無限成長而且可能填滿硬碟：  
  
-   DQS 資料庫的預設 **[自動成長]** 大小設定為 10%。  
  
-   DQS 資料庫的預設復原模式設定為 **[簡單]**。 在簡單復原模式中，交易會使用最低限度記錄，而且系統會在交易完成之後自動進行記錄截斷，以便釋出交易記錄 (.ldf 檔案) 中的空間。 如需簡單復原模式的詳細資訊，請參閱[完整資料庫備份 &#40;SQL Server&#41;](../relational-databases/backup-restore/full-database-backups-sql-server.md)。  
  
> [!IMPORTANT]  
>  -   在簡單復原模式中，當記錄檔記錄有一段很長的時間維持在使用中狀態 (例如，冗長且耗時的交易) 時，記錄截斷可能會延遲，因此可能會導致交易記錄填滿。 此外，記錄截斷不會縮減實體記錄檔 (.ldf 檔案) 的大小。 若要縮減實體記錄檔的大小，您必須壓縮記錄檔。 如需有關疑難排解交易記錄之相關問題的詳細資訊，請參閱[交易記錄 &#40;SQL Server&#41;](../relational-databases/logs/the-transaction-log-sql-server.md) 或位於 [http://go.microsoft.com/fwlink/?LinkId=237446](http://go.microsoft.com/fwlink/?LinkId=237446) 的 Microsoft 支援服務文件。  
> -   您必須定期執行 DQS 資料庫的完整或差異備份，並且備份交易記錄，以便執行資料的時間點復原。 如需詳細資訊，請參閱[完整資料庫備份 &#40;SQL Server&#41;](../relational-databases/backup-restore/full-database-backups-sql-server.md) 和[備份交易記錄 &#40;SQL Server&#41;](../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)。  
  
##  <a name="DetachAttach"></a> 卸離/附加 DQS 資料庫  
 您可以卸離 DQS 資料庫的資料檔和交易記錄檔，再將資料庫重新附加至相同或不同的 SQL Server 執行個體，藉此將 DQS 資料庫更換到相同電腦上的另一個 SQL Server 執行個體或是移動資料庫。  
  
 如需在 SQL Server 中卸離和附加資料庫之事前考量與操作期間注意事項的詳細資訊，請參閱[卸離和附加資料庫 &#40;SQL Server&#41;](../relational-databases/databases/database-detach-and-attach-sql-server.md)。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|描述如何備份及還原 DQS 資料庫。|[備份與還原 DQS 資料庫](../data-quality-services/backing-up-and-restoring-dqs-databases.md)|  
|描述如何卸離和附加 DQS 資料庫。|[中斷連線和附加 DQS 資料庫](../data-quality-services/detaching-and-attaching-dqs-databases.md)|  
  
## <a name="see-also"></a>另請參閱  
 [DQS 管理](../data-quality-services/dqs-administration.md)  
  
  

