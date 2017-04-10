---
title: "備份及還原複寫的資料庫 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "備份 [SQL Server 複寫]"
  - "管理複寫，還原"
  - "備份複寫的資料庫"
  - "備份 [SQL Server 複寫]，關於備份"
  - "還原複寫的資料庫 [SQL Server 複寫]"
  - "復原 [SQL Server 複寫]，關於復原"
  - "還原資料庫 [SQL Server]，複寫的資料庫"
  - "備份資料庫 [SQL Server]，複寫的資料庫"
  - "還原 [SQL Server 複寫]，關於還原"
  - "復原 [SQL Server 複寫]"
  - "複寫 [SQL Server]，管理"
  - "散發資料庫 [SQL Server 複寫]，備份"
  - "還原 [SQL Server 複寫]"
  - "管理複寫，備份"
ms.assetid: 04588807-21e7-4bbe-9727-b72f692cffa7
caps.latest.revision: 40
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 40
---
# 備份及還原複寫的資料庫
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  針對複寫的資料庫進行資料的備份與還原時，需要特別地注意。 本主題提供每種複寫類型的備份與還原策略之簡介資訊，以及取得詳細資訊的連結。  
  
 複寫支援將複寫資料庫還原到與原先建立備份的同一個伺服器與資料庫。 如果您將複寫資料庫的備份還原到另一個伺服器或資料庫，將無法保留複寫設定。 在這種情況下，您必須於還原備份後重新建立所有發行集與訂閱。  
  
> [!NOTE]  
>  如果使用記錄傳送，也可以將複寫的資料庫還原至待命伺服器。 如需詳細資訊，請參閱 [記錄傳送和複寫 & #40。SQL Server & #41;](../../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md)。  
  
 您應該定期備份複寫的資料庫及其相關聯的系統資料庫。 請備份下列資料庫：  
  
-   發行者端的發行集資料庫  
  
-   散發者端的散發資料庫  
  
-   每個訂閱者端的訂閱資料庫  
  
-   發行者、散發者及所有訂閱者端的 **master** 與 **msdb** 系統資料庫。 這些資料庫應與其他每個及相關的複寫資料庫同時備份。 例如，在您備份發行集資料庫的同時，在發行者端備份 **master** 與 **msdb** 資料庫。 還原發行集資料庫時，請確定 **master** 與 **msdb** 資料庫的複寫組態與設定和發行集資料庫一致。  
  
 如果您執行一般記錄備份，就必須在記錄備份中擷取任何複寫相關的變更。 如果不執行記錄備份，則每當與複寫相關的設定發生變更時，便應該執行備份。 如需詳細資訊，請參閱 [Common Actions Requiring an Updated Backup](../../../relational-databases/replication/administration/common-actions-requiring-an-updated-backup.md)。  
  
## 備份與還原策略  
 備份與還原複寫拓撲中每個節點的策略，會因所用的複寫類型而異。 如需每種複寫類型的備份與還原策略之詳細資訊，請參閱下列主題：  
  
-   [備份與還原快照式和異動複寫的策略](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)  
  
-   [備份與還原合併式複寫的策略](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-merge-replication.md)  
  
 請隨時將一份您現行複寫設定的指令碼存放在安全之處，作為復原策略的一部份。 如此一來，倘若伺服器發生錯誤或需要設定測試環境，您可藉由變更伺服器名稱參考來修改該指令碼，如此可幫助重新建立您的複寫設定。 除了將現行複寫設定撰寫成指令碼之外，您還必須撰寫可啟用及停用複寫的指令碼。 如需有關編寫複寫物件指令碼的詳細資訊，請參閱＜ [Scripting Replication](../../../relational-databases/replication/scripting-replication.md)＞。  
  
## 另請參閱  
 [SQL Server 資料庫的備份與還原](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [複寫管理的最佳做法](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)  
  
  