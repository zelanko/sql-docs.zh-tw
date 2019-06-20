---
title: 管理 DQS 使用者，在 SSMS 中的 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 955af01d-00da-4c51-9311-f3848749df54
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: eccb3ea2ec046a84a2735c310c8b80c5e88cf96e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65480341"
---
# <a name="manage-dqs-users-in-ssms"></a>在 SSMS 中管理 DQS 使用者
  此主題描述如何使用 SQL Server Management Studio 在 SQL Server 執行個體中建立其他使用者，並為其授與 DQS_MAIN 資料庫的適當 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 角色。  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 您的 Windows 使用者帳戶必須是適當固定伺服器角色 (例如 securityadmin、serveradmin 或 sysadmin) 的成員，才能建立 SQL 登入並授與適當的 DQS 角色。  
  
##  <a name="GrantRoles"></a> 建立 SQL 登入並授與 DQS 角色  
  
1.  啟動 Microsoft SQL Server Management Studio。  
  
2.  在 Microsoft SQL Server Management Studio 中，展開您的 SQL Server 執行個體，然後展開 **[安全性]**。  
  
3.  以滑鼠右鍵按一下 [安全性] 資料夾，並指向 [新增]，然後按一下 [登入]。  
  
4.  在 [登入 - 新增] 對話方塊的 [登入名稱] 方塊中，指定 Windows 使用者的名稱，指定 [Windows 驗證] 做為驗證類型，然後按一下 [搜尋] 驗證使用者。  
  
    > [!NOTE]  
    >  DQS 僅支援 Windows 驗證，不支援 SQL Server 驗證。  
  
5.  使用者驗證完成後，按一下左窗格中的 **[使用者對應]** 頁面。  
  
6.  在右窗格中，從 **DQS_MAIN** 資料庫的 [對應] 資料行底下選取該核取方塊，然後選取 **dqs_administrator**、**dqs_kb_editor** 或 **dqs_kb_operator** 核取方塊，這些核取方塊位於 [資料庫角色成員資格對象: DQS_MAIN] 窗格中，且根據使用者所需的存取層級來選取。  
  
7.  在 [登入 - 新增] 對話方塊中，按一下 [確定] 套用變更。  
  
    > [!NOTE]  
    >  如果您對使用者授與 **dqs_administrator** 角色並套用了變更，然後重新檢查使用者的權限，也會同時選取另外兩個 DQS 角色核取方塊 (**dq_kb_editor** 和 **dqs_kb_operator**)。  
  
  
