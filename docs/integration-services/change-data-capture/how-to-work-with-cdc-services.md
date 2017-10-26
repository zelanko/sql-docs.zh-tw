---
title: "如何使用 CDC 服務 |Microsoft 文件"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: db5c718a-6e7f-48ec-82a3-9d5b131716e5
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bd4d1ea9deb9451701f84470ed2f35f7aa220df2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/28/2017

---
# <a name="how-to-work-with-cdc-services"></a>如何使用 CDC 服務
  這個程序描述如何使用 CDC 服務組態主控台來準備 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，以便使用 Oracle CDC 服務及建立新的 CDC 服務。  
  
### <a name="to-work-with-cdc-services"></a>若要使用 CDC 服務  
  
1.  從 **[開始]** 功能表，選取 **[Oracle CDC 服務組態]**。  
  
2.  從左窗格選取 [本機 CDC 服務]\(根層級)。  
  
3.  您會執行下列其中一項或兩項工作：  
  
    -   **準備 SQL Server**  
  
         從 CDC 服務組態主控台右側的 **[動作]** 窗格中選取這個選項。  
  
         您也可以用滑鼠右鍵按一下 [本機 CDC 服務]，並選取 [準備 SQL Server]。  
  
         隨即開啟 [為 Oracle CDC 準備 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體] 對話方塊。  
  
         若要為 Oracle CDC 服務準備 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，登入必須擁有具備 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 固定伺服器角色的 `dbcreator` 登入。 此登入是用來建立加入 Oracle CDC 服務以及之後加入 Oracle CDC 執行個體所需的 MSXDBCDC 資料庫。  
  
         如需有關如何使用此對話方塊的詳細資訊，請參閱＜ [Prepare SQL Server for CDC](../../integration-services/change-data-capture/prepare-sql-server-for-cdc.md)＞。 如需如何針對 CDC 啟用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的資訊，請參閱 [如何為 CDC 準備 SQL Server](../../integration-services/change-data-capture/how-to-prepare-sql-server-for-cdc.md)。  
  
    -   **建立新的 CDC 服務**  
  
         從 CDC 服務組態主控台右側的 **[動作]** 窗格中按一下 **[新增服務]** 。  
  
         您也可以用滑鼠右鍵按一下 [本機 CDC 服務]，並選取 [新增服務]。  
  
         隨即開啟 [新增 Oracle CDC 服務] 對話方塊。  
  
         如需有關如何使用此對話方塊的詳細資訊，請參閱＜ [Create and Edit an Oracle CDC Service](../../integration-services/change-data-capture/create-and-edit-an-oracle-cdc-service.md)＞。 如需有關如何建立或編輯 CDC 服務的詳細資訊，請參閱＜ [How to Create and Edit a CDC Service](../../integration-services/change-data-capture/how-to-create-and-edit-a-cdc-service.md)＞。  
  
         Oracle CDC 服務所使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入只要求它必須是 `public` 固定伺服器角色的成員，不需要其他權限。 但是，若要建立 Oracle CDC 服務，此登入必須擁有 MSXDBCDC 資料庫的寫入權限，例如 **db_owner** 資料庫角色必須指派給此登入。 當沒有 MSXDBDCDC 資料庫寫入權限的登入嘗試建立新的 Oracle CDC 執行個體時，便會顯示錯誤訊息。 在這個對話方塊中按一下 **[確定]** ，隨即顯示 [連接到 SQL Server] 對話方塊。  
  
         如需如何輸入擁有 MSXDBCDC 資料庫寫入權限之登入認證的資訊，例如 **db_owner** 資料庫角色，請參閱 [建立及編輯 Oracle CDC 服務](../../integration-services/change-data-capture/create-and-edit-an-oracle-cdc-service.md) 和 [連接到 SQL Server](../../integration-services/change-data-capture/connection-to-sql-server.md)。  
  
## <a name="see-also"></a>另請參閱  
 [使用 CDC 服務](../../integration-services/change-data-capture/work-with-cdc-services.md)  
  
  

