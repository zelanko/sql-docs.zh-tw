---
title: 管理原則類別目錄 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.dmf.policycategories.f1
ms.assetid: d188a819-731f-4029-98aa-780d3299a0ce
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 6f0600f663e00e0318a933e7824f3e0b78166f55
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68087189"
---
# <a name="manage-policy-categories"></a>管理原則類別目錄
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，將某個類別目錄中的任何或所有可用原則套用至 [!INCLUDE[tsql](../../includes/tsql-md.md)]的整個執行個體。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **若要使用下列方法將類別目錄原則套用至 SQL Server 執行個體：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]時，如果未選取 **[託管資料庫訂閱]** 核取方塊，原則類別目錄必須個別套用到伺服器的每一個相關部分，例如一個或多個資料庫或資料表。  
  
-   如果您指定不存在的原則類別目錄，就會建立新的原則類別目錄，而且當您執行此預存程序時，所有資料庫都會託管此訂閱。 如果您之後針對新的類別目錄清除託管的訂閱，只會針對您指定為 *target_object*的資料庫來套用此訂閱。 如需如何變更授權之訂閱設定的詳細資訊，請參閱 [sp_syspolicy_update_policy_category &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-update-policy-category-transact-sql.md)。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 此預存程序會在目前預存程序擁有者的內容中執行。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-apply-category-policies-to-a-sql-server-instance"></a>若要將類別目錄原則套用至 SQL Server 執行個體  
  
1.  在 **[物件總管]** 中，按一下加號展開要套用類別目錄原則的伺服器。  
  
2.  按一下加號展開 **[管理]** 資料夾。  
  
3.  以滑鼠右鍵按一下 [原則管理]  並選取 [管理類別目錄]  。  
  
     **[管理原則類別目錄]** 對話方塊中提供下列資訊：  
  
     **名稱**  
     原則類別目錄的名稱。  
  
     **[託管資料庫訂閱]**  
     強制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上的所有資料庫強制施行原則類別目錄中的原則。  
  
4.  選取或清除 **[託管資料庫訂閱]** 下的任何或所有核取方塊，將該原則類別目錄套用至 SQL Server 執行個體。  
  
5.  完成後，請按一下 **[確定]** 。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-apply-category-policies-to-a-sql-server-instance"></a>若要將類別目錄原則套用至 SQL Server 執行個體  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
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
  
  
