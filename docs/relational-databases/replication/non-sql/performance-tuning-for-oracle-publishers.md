---
title: Oracle 發行者的效能微調 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], performance tuning
ms.assetid: 32c0b4ec-c166-45a3-b41e-38a30fd56813
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a5ae003e6d8a9d13ac9b0d6b9dfa99a497a26c23
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47595509"
---
# <a name="performance-tuning-for-oracle-publishers"></a>Oracle 發行者的效能微調
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Oracle 發行架構與 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 發行架構相似；因此，微調 Oracle 複寫效能的第一步需要按照 [Enhance General Replication Performance](../../../relational-databases/replication/administration/enhance-general-replication-performance.md)中的一般微調建議進行。  
  
 此外，還提供了兩個與效能有關的「Oracle 發行者」選項：  
  
-   指定適當的發行選項：[Oracle] 或 [Oracle 閘道]。  
  
-   設定交易集作業，以便用適當的間隔處理「發行者」端的變更。  
  
## <a name="specifying-the-appropriate-publishing-option"></a>指定適當的發行選項  
 Oracle Gateway 選項提供比 Oracle Complete 選項更好的效能；不過此選項不可用於多個交易式發行集內發行同一資料表。 資料表最多可以出現在單一交易式發行集，以及任意多個快照集發行集內。 若您需要在多個交易式發行集內發行同一資料表，請選擇 Oracle Complete 選項。 在「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者」端識別「Oracle 發行者」時，請指定此選項。 如需詳細資訊，請參閱 [Create a Publication from an Oracle Database](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)。  
  
## <a name="configuring-the-transaction-set-job"></a>設定交易集作業  
 已發行的 Oracle 資料表之變更會以群組 (稱為交易集) 方式進行處理。 為確保交易一致性，每個交易集在散發資料庫中均視為單一交易。 如果交易集變得很大，則無法視為單一交易進行有效地處理。  
  
 依預設，交易集只能由「記錄讀取器代理程式」建立。 如果在頻繁變更活動期間，「記錄讀取器代理程式」未執行，或無法從「 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者」連接到「Oracle 發行者」，則交易集會變得巨大而無法管理。 若要防止出現此問題，請確定定期建立交易集，即使「記錄讀取器代理程式」未執行或無法連接到「Oracle 發行者」。  
  
 交易集可以使用 Xactset 作業 (由複寫安裝的 Oracle 資料庫作業) 來建立，Xactset 作業使用與「記錄讀取器代理程式」相同的機制建立交易集。 每次執行此作業時，均會建立一個新的交易集。 下次執行「記錄讀取器代理程式」時，代理程式會處理所有已建立的任一交易集。 如果在處理完全部現有交易集後仍有擱置的變更，「記錄讀取器代理程式」會建立並處理一個或多個額外的交易集。  
  
 若要設定交易集作業，請參閱[設定 Oracle 發行者的交易集作業 &#40;複寫 Transact-SQL 程式設計&#41;](../../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)。  
  
## <a name="see-also"></a>另請參閱  
 [設定 Oracle 發行者](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Oracle 發行概觀](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
