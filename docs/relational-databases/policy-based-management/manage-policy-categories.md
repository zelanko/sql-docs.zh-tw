---
title: "管理原則類別目錄 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.dmf.policycategories.f1
ms.assetid: d188a819-731f-4029-98aa-780d3299a0ce
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 952740a7191b43f61f9cff035b0ad944fe802084
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="manage-policy-categories"></a>管理原則類別目錄
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，將某個類別目錄中的任何或所有可用原則套用至 [!INCLUDE[tsql](../../includes/tsql-md.md)]的整個執行個體。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要使用下列方法將類別目錄原則套用至 SQL Server 執行個體：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]時，如果未選取 **[託管資料庫訂閱]** 核取方塊，原則類別目錄必須個別套用到伺服器的每一個相關部分，例如一個或多個資料庫或資料表。  
  
-   如果您指定不存在的原則類別目錄，就會建立新的原則類別目錄，而且當您執行此預存程序時，所有資料庫都會託管此訂閱。 如果您之後針對新的類別目錄清除託管的訂閱，只會針對您指定為 *target_object* 的資料庫來套用此訂閱。 如需如何變更授權之訂閱設定的詳細資訊，請參閱 [sp_syspolicy_update_policy_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-update-policy-category-transact-sql.md)。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 此預存程序會在目前預存程序擁有者的內容中執行。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-apply-category-policies-to-a-sql-server-instance"></a>若要將類別目錄原則套用至 SQL Server 執行個體  
  
1.  在 **[物件總管]**中，按一下加號展開要套用類別目錄原則的伺服器。  
  
2.  按一下加號展開 **[管理]** 資料夾。  
  
3.  以滑鼠右鍵按一下 [原則管理] 並選取 [管理類別目錄]。  
  
     **[管理原則類別目錄]** 對話方塊中提供下列資訊：  
  
     **名稱**  
     原則類別目錄的名稱。  
  
     **[託管資料庫訂閱]**  
     強制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上的所有資料庫強制施行原則類別目錄中的原則。  
  
4.  選取或清除 **[託管資料庫訂閱]** 下的任何或所有核取方塊，將該原則類別目錄套用至 SQL Server 執行個體。  
  
5.  完成後，請按一下 **[確定]**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-apply-category-policies-to-a-sql-server-instance"></a>若要將類別目錄原則套用至 SQL Server 執行個體  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  將下列範例複製並貼入查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    USE msdb;  
    GO  
    -- configures the specified database to subscribe to a policy category that is named 'Table Naming Policies'.  
    EXEC dbo.sp_syspolicy_add_policy_category_subscription @target_type = N'DATABASE'  
    , @target_object = N'AdventureWorks2012'  
    , @policy_category = N'Table Naming Policies';  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [sp_syspolicy_add_policy_category_subscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-add-policy-category-subscription-transact-sql.md)。  
  
  

