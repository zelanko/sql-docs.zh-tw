---
title: 訂閱者 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.subscribers.f1
helpviewer_keywords:
- Subscribers [SQL Server replication]
ms.assetid: 43fb2454-c220-4d25-a826-83c332eb00d2
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 6988274ce4c8f8bf38d89c156150b37589529dae
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769474"
---
# <a name="subscribers"></a>訂閱者
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  指定會接收所選發行集訂閱的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者。


[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]
  
## <a name="options"></a>選項。  
 **[發行者屬性]**  
 選取方格中的核取方塊以啟用對應的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來源，作為 [發行集]  頁面上所選發行集的訂閱者。 如果未列出訂閱者，請按一下 **[加入訂閱者]** 或 **[加入 SQL Server 訂閱者]** 。  
  
 **訂閱資料庫**  
 此資料行中顯示的資訊和可用的動作，會視 **[訂閱者]** 資料行中所列出的訂閱者類型而定：  
  
-   針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者，請從 **[訂閱資料庫]** 清單中選取訂閱資料庫，或從相同清單中選取 **[新增資料庫]** 命令來建立新的資料庫。  
  
    > [!NOTE]  
    >  如果您啟用發行者作為訂閱者，則訂閱資料庫必須不同於發行集資料庫。  
  
-   針對非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者，不會顯示訂閱資料庫。 在 **[加入非 SQL Server]** 對話方塊的 **[資料來源名稱]** 欄位中，指定資料庫以及其他連接資訊。 按一下 **[加入訂閱者]** 然後按一下 **[加入非 SQL Server 訂閱者]** ，即可使用此對話方塊。  
  
 **[加入訂閱者]**  
 將伺服器加入可以啟用為訂閱者的伺服器清單中。 當所有下列條件都為 True 時，會顯示此按鈕：  
  
-   選取的發行集是不支援更新訂閱的快照式發行集或交易式發行集。  
  
    > [!NOTE]  
    >  如果您所訂閱的發行集擁有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的訂閱，而發行集尚未啟用給非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者使用，則您無法新增非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的訂閱。  
  
-   訂閱是發送訂閱。  
  
-   選取之發行集的發行者是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更新的版本。  
  
 按一下 [新增訂閱者]  就會顯示具有兩個選項的功能表：[新增 SQL Server 訂閱者]  和 [新增非 SQL Server 訂閱者]  。 按一下 **[加入非 SQL Server 訂閱者]** ，即可加入 Oracle 或 IBM DB2 訂閱者。  
  
 **[加入 SQL Server 訂閱者]**  
 將伺服器加入可以啟用為訂閱者的伺服器清單中。 當一或多個下列條件為 True 時，會顯示此按鈕：  
  
-   選取的發行集是合併式發行集，或支援更新訂閱的快照式發行集或交易式發行集。  
  
-   訂閱是提取訂閱。  
  
-   選取之發行集的發行者是 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]之前的版本。 針對先前的版本，只有當一或多個下列條件為 True 時，才會顯示此按鈕：  
  
    -   您是發行者端 **系統管理員** (sysadmin) 固定伺服器角色的成員。  
  
    -   訂閱者已經加入 **[發行者屬性]** 對話方塊中的 **[訂閱者]** 頁面上。  
  
    -   發行集允許匿名訂閱。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [訂閱發行集](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
