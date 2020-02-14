---
title: Oracle 發行相關術語字彙 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], glossary
ms.assetid: e21dfa4b-6144-4be7-9cbf-ca2709b2bd9f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8ac643b3c0c095dee143c3feca878bd4072273bb
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "67901105"
---
# <a name="glossary-of-terms-for-oracle-publishing"></a>Oracle 發行相關術語字彙
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在設定與管理 Oracle 發行時，應熟悉下列 Oracle 術語。 如需完整的 Oracle 術語清單，請參閱 Oracle 線上文件集。  
  
#### <a name="index-organized-tables-iot"></a>按索引組織的資料表 (IOT)  
 其資料按索引順序實際儲存在磁碟中的資料表；類似於具有叢集索引的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料表。 將 IOT 做為具有叢集索引的資料表複寫到「訂閱者」。  
  
#### <a name="instance"></a>執行個體  
 Oracle 資料庫與執行個體相關聯。 執行個體包含記憶體與支援資料庫的背景處理序。 Oracle 執行個體始終對應到單一資料庫，而 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的執行個體可能包含多個資料庫。 也存在一個 Oracle 資料庫含有多個執行個體的情況。  
  
#### <a name="oracle-listener"></a>Oracle 接聽程式  
 處理 Oracle 資料庫執行個體的連入網路流量。 在設定到 Oracle 資料庫的網路連接時，您需指定用來傳送流量的通訊協定以及接聽程式接聽流量的通訊埠。 接聽程式通常設定為在與 Oracle 資料庫執行個體所處電腦相同的電腦上執行，還可以設定為服務於一個或多個執行個體。  
  
#### <a name="rowid"></a>ROWID  
 指向資料庫中特定資料列位置的指標。 因為使用 ROWID 擷取資料列比使用資料表掃描或索引要快，所以複寫在處理已發行的資料表變更時暫時使用 ROWID。  
  
#### <a name="sequence"></a>順序  
 用來產生唯一數字的資料庫物件。 複寫使用序列對已發行資料表的變更進行排序。  
  
#### <a name="sqlplus"></a>SQL\*Plus  
 用來存取與查詢 Oracle 資料庫的應用程式。 類似於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **sqlcmd**。  
  
#### <a name="synonym"></a>同義字  
 物件的別名。 在設定「Oracle 發行者」時會自動建立特殊的公用同義字 **MSSQLSERVERDISTRIBUTOR** 。 同義字參考 **HREPL_Distributor** 資料表，並提供指向服務於「發行者」之「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者」的邏輯指標。  
  
 發行 Oracle 資料庫之後，就無法將此「發行者」設定為使用不同的「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者」，因為此公用同義字識別出已將特定「散發者」設定為服務於「發行者」。  
  
#### <a name="tablespace"></a>資料表空間  
 資料庫的儲存單位，大致相當於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中的檔案群組。  
  
#### <a name="tns-service-name"></a>TNS 服務名稱  
 TNS (Transparent Network Substrate) 是 Oracle 資料庫所使用的通訊層。 TNS Service Name 是 Oracle 資料庫執行個體在網路上使用的名稱。 您可以在為 Oracle 資料庫設定連接時，指派 TNS Service Name。 複寫使用「TNS 服務」名稱來識別「發行者」並建立連接。  
  
#### <a name="user-schema"></a>使用者結構描述  
 可以將使用者結構描述想像成擁有特定資料庫物件集的資料庫使用者。 複寫管理的使用者結構描述在 Oracle 資料庫中擁有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 複寫處理所建立的所有物件，但公用同義字 **MSSQLSERVERDISTRIBUTOR** 除外。  
  
## <a name="see-also"></a>另請參閱  
 [設定 Oracle 發行者](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [在 Oracle 發行者上建立的物件](../../../relational-databases/replication/non-sql/objects-created-on-the-oracle-publisher.md)   
 [非 SQL Server 發行者](../../../relational-databases/replication/non-sql/non-sql-server-publishers.md)   
 [Oracle 發行概觀](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
