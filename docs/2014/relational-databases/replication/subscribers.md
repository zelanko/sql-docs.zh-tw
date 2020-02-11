---
title: 訂閱者 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.subscribers.f1
helpviewer_keywords:
- Subscribers [SQL Server replication]
ms.assetid: 43fb2454-c220-4d25-a826-83c332eb00d2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 725be263e30687a3f2ded90990e952e1cd97a185
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62629392"
---
# <a name="subscribers"></a>訂閱者
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]指定將接收所選[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行集之訂閱的或非訂閱者。  
  
## <a name="options"></a>選項。  
 **[發行者屬性]**  
 選取方格中的核取方塊，讓對應[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的或非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料來源成為**發行**集頁面上選擇之發行集的訂閱者。 如果未列出訂閱者，請按一下 **[加入訂閱者]** 或 **[加入 SQL Server 訂閱者]**。  
  
 **訂閱資料庫**  
 此資料行中顯示的資訊和可用的動作，會視 **[訂閱者]** 資料行中所列出的訂閱者類型而定：  
  
-   針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者，請從 **[訂閱資料庫]** 清單中選取訂閱資料庫，或從相同清單中選取 **[新增資料庫]** 命令來建立新的資料庫。  
  
    > [!NOTE]  
    >  如果您啟用發行者作為訂閱者，則訂閱資料庫必須不同於發行集資料庫。  
  
-   針對非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者，不會顯示訂閱資料庫。 在 **[加入非 SQL Server]** 對話方塊的 **[資料來源名稱]** 欄位中，指定資料庫以及其他連接資訊。 按一下 **[加入訂閱者]** 然後按一下 **[加入非 SQL Server 訂閱者]**，即可使用此對話方塊。  
  
 **新增訂閱者**  
 將伺服器加入可以啟用為訂閱者的伺服器清單中。 當所有下列條件都為 True 時，會顯示此按鈕：  
  
-   選取的發行集是不支援更新訂閱的快照式發行集或交易式發行集。  
  
    > [!NOTE]  
    >  如果您所訂閱的發行集擁有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的訂閱，而發行集尚未啟用給非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者使用，則您無法新增非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的訂閱。  
  
-   訂閱是發送訂閱。  
  
-   選取之發行集的發行者是[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]或更新版本。  
  
 按一下 **[加入訂閱者]** 會顯示包含下列兩個選項的功能表： **[加入 SQL Server 訂閱者]** 和 **[加入非 SQL Server 訂閱者]**。 按一下 **[加入非 SQL Server 訂閱者]** ，即可加入 Oracle 或 IBM DB2 訂閱者。  
  
 **新增 SQL Server 訂閱者**  
 將伺服器加入可以啟用為訂閱者的伺服器清單中。 當一或多個下列條件為 True 時，會顯示此按鈕：  
  
-   選取的發行集是合併式發行集，或支援更新訂閱的快照式發行集或交易式發行集。  
  
-   訂閱是提取訂閱。  
  
-   選取之發行集的發行者是 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]之前的版本。 針對先前的版本，只有當一或多個下列條件為 True 時，才會顯示此按鈕：  
  
    -   您是發行者端 **系統管理員** (sysadmin) 固定伺服器角色的成員。  
  
    -   訂閱者已經加入 **[發行者屬性]** 對話方塊中的 **[訂閱者]** 頁面上。  
  
    -   發行集允許匿名訂閱。  
  
## <a name="see-also"></a>另請參閱  
 [Create a Pull Subscription](create-a-pull-subscription.md)   
 [Create a Push Subscription](create-a-push-subscription.md)   
 [非 SQL Server 訂閱者](non-sql/non-sql-server-subscribers.md)   
 [訂閱發行集](subscribe-to-publications.md)  
  
  
