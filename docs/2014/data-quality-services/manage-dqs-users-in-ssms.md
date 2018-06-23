---
title: 管理 DQS 使用者，在 SSMS 中的 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 955af01d-00da-4c51-9311-f3848749df54
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: a6115b9b28b4c27c6b3cddccd1f83ec1aef02ab3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145465"
---
# <a name="manage-dqs-users-in-ssms"></a>在 SSMS 中管理 DQS 使用者
  此主題描述如何使用 SQL Server Management Studio 在 SQL Server 執行個體中建立其他使用者，並為其授與 DQS_MAIN 資料庫的適當 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 角色。  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 您的 Windows 使用者帳戶必須是適當固定伺服器角色 (例如 securityadmin、serveradmin 或 sysadmin) 的成員，才能建立 SQL 登入並授與適當的 DQS 角色。  
  
##  <a name="GrantRoles"></a> 建立 SQL 登入及授與 DQS 角色  
  
1.  啟動 Microsoft SQL Server Management Studio。  
  
2.  在 Microsoft SQL Server Management Studio 中，展開您的 SQL Server 執行個體，然後展開 **[安全性]**。  
  
3.  以滑鼠右鍵按一下 **[安全性]** 資料夾、指向 **[新增]**，再按一下 **[登入]**。  
  
4.  在 **[登入 - 新增]** 對話方塊的 **[登入名稱]** 方塊中，指定 Windows 使用者的名稱，指定 **[Windows 驗證]** 做為驗證類型，然後按一下 **[搜尋]** 驗證使用者。  
  
    > [!NOTE]  
    >  DQS 僅支援 Windows 驗證，不支援 SQL Server 驗證。  
  
5.  使用者驗證完成後，按一下左窗格中的 **[使用者對應]** 頁面。  
  
6.  根據使用者所需的存取層級，在右邊的窗格中，從 **DQS_MAIN** 資料庫的 **[地圖]** 欄選取該核取方塊，然後選取 **dqs_administrator**、 **dqs_kb_editor**或 **[資料庫角色成員資格對象: DQS_MAIN]** 窗格中的 **dqs_kb_operator** 核取方塊。  
  
7.  在 **[登入 - 新增]** 對話方塊中，按一下 **[確定]** 套用變更。  
  
    > [!NOTE]  
    >  如果您對使用者授與 **dqs_administrator** 角色並套用了變更，然後重新檢查使用者的權限，也會同時選取另外兩個 DQS 角色核取方塊 (**dq_kb_editor** 與 **dqs_kb_operator**) 。  
  
  