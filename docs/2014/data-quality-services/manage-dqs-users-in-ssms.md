---
title: 在 SSMS 中管理 DQS 使用者 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 955af01d-00da-4c51-9311-f3848749df54
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: bf4cd7cfb635aa990cbabab37905dd640f9e69fe
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84937509"
---
# <a name="manage-dqs-users-in-ssms"></a>在 SSMS 中管理 DQS 使用者
  此主題描述如何使用 SQL Server Management Studio 在 SQL Server 執行個體中建立其他使用者，並為其授與 DQS_MAIN 資料庫的適當 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 角色。  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 您的 Windows 使用者帳戶必須是適當固定伺服器角色 (例如 securityadmin、serveradmin 或 sysadmin) 的成員，才能建立 SQL 登入並授與適當的 DQS 角色。  
  
##  <a name="create-a-sql-login-and-grant-dqs-role"></a><a name="GrantRoles"></a>建立 SQL 登入並授與 DQS 角色  
  
1.  啟動 Microsoft SQL Server Management Studio。  
  
2.  在 Microsoft SQL Server Management Studio 中，展開您的 SQL Server 執行個體，然後展開 **[安全性]**。  
  
3.  以滑鼠右鍵按一下 [安全性]**** 資料夾，並指向 [新增]****，然後按一下 [登入]****。  
  
4.  在 [登入 - 新增]**** 對話方塊的 [登入名稱]**** 方塊中，指定 Windows 使用者的名稱，指定 [Windows 驗證]**** 做為驗證類型，然後按一下 [搜尋]**** 驗證使用者。  
  
    > [!NOTE]  
    >  DQS 僅支援 Windows 驗證，不支援 SQL Server 驗證。  
  
5.  使用者驗證完成後，按一下左窗格中的 **[使用者對應]** 頁面。  
  
6.  根據使用者所需的存取層級，在右邊的窗格中，從 **DQS_MAIN** 資料庫的 [地圖]**** 資料行選取該核取方塊，然後選取 [資料庫角色成員資格對象: DQS_MAIN]**** 窗格中的 **dqs_administrator**、**dqs_kb_editor** 或 **dqs_kb_operator** 核取方塊。  
  
7.  在 [登入 - 新增]**** 對話方塊中，按一下 [確定]**** 套用變更。  
  
    > [!NOTE]  
    >  如果您對使用者授與 **dqs_administrator** 角色並套用了變更，然後重新檢查使用者的權限，也會同時選取另外兩個 DQS 角色核取方塊 (**dq_kb_editor** 和 **dqs_kb_operator**)。  
  
  
