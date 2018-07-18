---
title: 從複寫監視器新增及移除發行者 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Replication Monitor, adding and removing Publishers
ms.assetid: fa36c4b4-bfa5-494e-92e3-07a02d7332c3
caps.latest.revision: 37
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c7f8cbded499127107802136d2d2e4503cef24ad
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37324218"
---
# <a name="add-and-remove-publishers-from-replication-monitor"></a>從複寫監視器加入及移除發行者
  從中啟動「複寫監視器」的伺服器會自動新增至監視器 (如果它是「發行者」)。 其他「發行者」可透過 **[加入發行者]** 對話方塊來新增。 在新增「發行者」之後，它會顯示在監視器左窗格的群組中。 依預設會包括 **[我的發行者]** 群組，但您可以建立新的群組來管理一個或多個複寫拓撲。 如需啟動複寫監視器的詳細資訊，請參閱[啟動複寫監視器](start-the-replication-monitor.md)。  
  
### <a name="to-add-a-sql-server-publisher"></a>若要新增 SQL Server 發行者  
  
1.  以滑鼠右鍵按一下左窗格裡的 **[複寫監視器]** 節點或發行者群組節點，然後按一下 **[加入發行者]**。  
  
2.  在 **[加入發行者]** 對話方塊中，按一下 **[加入]**，然後按一下 **[加入 SQL Server 發行者]**。  
  
3.  在 **[連接到伺服器]** 對話方塊中，輸入「發行者」的名稱，然後選取驗證類型。 如果您選取 **[SQL Server 驗證]**，請輸入登入與密碼。 複寫監視器會儲存您指定的認證，在未來連接到這個伺服器時使用。 指定的 Windows 帳戶或 SQL Server 登入必須是 **系統管理員 (sysadmin)** 固定伺服器角色的成員，或者散發資料庫中 **replmonitor** 固定資料庫角色的成員。  
  
4.  按一下 **[連接]**。 如果「發行者」使用遠端「散發者」，將會提示您在 **[連接到伺服器]** 對話方塊中連接到「散發者」。 複寫監視器會儲存您指定的認證，在未來連接到這個伺服器時使用。 指定的 Windows 帳戶或 SQL Server 登入必須是 **系統管理員 (sysadmin)** 固定伺服器角色的成員，或者散發資料庫中 **replmonitor** 固定資料庫角色的成員。  
  
5.  發行者與散發者的名稱會在 **[開始監視下列發行者]** 方格中顯示。  
  
6.  若要指定發行者的重新整理與連接選項，請從方格中選取發行者，然後依需要修改選項。 如需有關重新整理選項的詳細資訊，請參閱＜ [Caching, Refresh, and Replication Monitor Performance](caching-refresh-and-replication-monitor-performance.md)＞。  
  
7.  選取發行者應在複寫監視器中顯示的群組。 若要建立新群組，請按一下 **[新增群組]**，然後輸入群組名稱；從 **[在下列群組中顯示此發行者]** 清單裡選取群組。  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-add-an-oracle-publisher"></a>若要新增 Oracle 發行者  
  
1.  以滑鼠右鍵按一下左窗格裡的 **[複寫監視器]** 節點或發行者群組節點，然後按一下 **[加入發行者]**。  
  
2.  在 **[加入發行者]** 對話方塊中，按一下 **[加入]**，然後按一下 **[加入 Oracle 發行者]**。  
  
3.  在 **[連接到伺服器]** 對話方塊中，輸入與「Oracle 發行者」關聯的「 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 散發者」的名稱，然後選取驗證類型。 如果您選取 **[SQL Server 驗證]**，請輸入登入與密碼。 複寫監視器會儲存您指定的認證，在未來連接到這個伺服器時使用。 指定的 Windows 帳戶或 SQL Server 登入必須是 **系統管理員 (sysadmin)** 固定伺服器角色的成員，或者散發資料庫中 **replmonitor** 固定資料庫角色的成員。  
  
4.  按一下 **[連接]**。  
  
5.  發行者與散發者的名稱會在 **[開始監視下列發行者]** 方格中顯示。  
  
6.  若要指定發行者的重新整理與連接選項，請從方格中選取發行者，然後依需要修改選項。 如需有關重新整理選項的詳細資訊，請參閱＜ [Caching, Refresh, and Replication Monitor Performance](caching-refresh-and-replication-monitor-performance.md)＞。  
  
7.  選取發行者應在複寫監視器中顯示的群組。 若要建立新群組，請按一下 **[新增群組]**，然後輸入群組名稱；從 **[在下列群組中顯示此發行者]** 清單裡選取群組。  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-add-one-or-more-publishers-that-use-the-same-distributor"></a>若要新增一個或多個使用相同散發者的發行者  
  
1.  以滑鼠右鍵按一下左窗格裡的 **[複寫監視器]** 節點或發行者群組節點，然後按一下 **[加入發行者]**。  
  
2.  在 **[加入發行者]** 對話方塊中，按一下 **[加入]**，然後按一下 **[指定散發者，並加入其發行者]**。  
  
3.  在 **[連接到伺服器]** 對話方塊中，輸入「散發者」的名稱，然後選取驗證類型。 如果您選取 **[SQL Server 驗證]**，請輸入登入與密碼。 複寫監視器會儲存您指定的認證，在未來連接到這個伺服器時使用。 指定的 Windows 帳戶或 SQL Server 登入必須是 **系統管理員 (sysadmin)** 固定伺服器角色的成員，或者散發資料庫中 **replmonitor** 固定資料庫角色的成員。  
  
4.  按一下 **[連接]**。  
  
5.  「散發者」與每個「發行者」的名稱顯示在 **[開始監視下列發行者]** 方格中。 如果「發行者」已新增至「複寫監視器」，則不會顯示在方格中。  
  
6.  若要指定發行者的重新整理與連接選項，請從方格中選取發行者，然後依需要修改選項。 如需有關重新整理選項的詳細資訊，請參閱＜ [Caching, Refresh, and Replication Monitor Performance](caching-refresh-and-replication-monitor-performance.md)＞。  
  
7.  選取在「複寫監視器」中應顯示「發行者」的群組。 若要建立新群組，請按一下 **[新增群組]**，然後輸入群組名稱；從 **[在下列群組中顯示此發行者]** 清單裡選取群組。  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-modify-settings-for-the-publisher-and-publisher-groups"></a>若要修改發行者與發行者群組的設定  
  
1.  以滑鼠右鍵按一下左窗格中的「發行者」，然後按一下 **[發行者設定]**。  
  
2.  在 **[發行者設定]** 對話方塊中進行任何變更：  
  
    -   若要變更「複寫監視器」用來連接到伺服器的認證，請按一下 **[發行者連接]** 或 **[散發者連接]**，然後在 **[連接到伺服器]** 對話方塊中輸入認證。  
  
    -   若要將某「發行者」從一個群組移至另一個群組，請在 **[開始監視下列發行者]** 方格中選取該「發行者」，然後在 **[在下列群組中顯示此發行者]** 清單中選取新群組。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-remove-a-publisher-from-replication-monitor"></a>若要從複寫監視器移除發行者  
  
1.  以滑鼠右鍵按一下左窗格中的「發行者」：  
  
2.  按一下 **[移除]**。  
  
### <a name="to-add-a-publisher-group-to-replication-monitor"></a>若要新增發行者群組至複寫監視器  
  
1.  發行者群組僅在新增「發行者」或修改「發行者」的設定時才可建立。 請參閱新增「發行者」的「如何」程序，以取得詳細資訊。  
  
### <a name="to-remove-a-publisher-group-from-replication-monitor"></a>若要從複寫監視器移除發行者群組  
  
1.  將所有「發行者」移至另一個群組或從「複寫監視器」移除它們。 如需詳細資訊，請參閱本主題前文中的程序。  
  
2.  以滑鼠右鍵按一下「發行者」群組，然後按一下 **[移除]**。  
  
## <a name="see-also"></a>另請參閱  
 [[設定散發]](../configure-distribution.md)   
 [監視複寫](../monitoring-replication.md)  
  
  
