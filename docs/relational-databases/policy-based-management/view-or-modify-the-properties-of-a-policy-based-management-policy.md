---
title: 檢視或修改原則式管理原則的屬性 | Microsoft 文件
ms.custom: ''
ms.date: 10/06/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Policy-Based Management, modify policies
- Policy-Based Management, view policies
ms.assetid: ba805504-5db5-4731-a8da-a0e89cb20c37
caps.latest.revision: 9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b90bf92f009d2d47565723b3ff0f7fac3fbebb35
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="view-or-modify-the-properties-of-a-policy-based-management-policy"></a>檢視或修改原則式管理原則的屬性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中檢視或修改原則式管理原則的屬性。  
  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
  
####  <a name="Permissions"></a> 權限  
 需要 msdb 資料庫中 PolicyAdministratorRole 角色的成員資格。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-the-properties-of-all-policies-on-an-object"></a>若要檢視物件之所有原則的屬性  
  
1.  在物件總管中，以滑鼠右鍵按一下伺服器、伺服器物件、資料庫或資料庫物件，指向 [原則]，然後選取 [檢視]。 如需 [檢視原則 - <物件名稱>] 對話方塊可用之選項的詳細資訊，請參閱[檢視原則對話方塊](../../relational-databases/policy-based-management/view-policies-dialog-box.md)。  
  
2.  完成後，請按一下 **[關閉]**。  
  
#### <a name="to-view-or-modify-a-specific-policys-properties"></a>若要檢視或修改特定原則的屬性  
  
1.  在 **物件總管**中，按一下加號，展開包含您想要檢視或修改之原則式管理原則的伺服器。  
  
2.  按一下加號展開 **[管理]** 資料夾。  
  
3.  按一下加號展開 **[原則管理]**。  
  
4.  按一下加號展開 **[原則]** 資料夾。  
  
5.  以滑鼠右鍵按一下您想要檢視或修改的原則，然後選取 [屬性]。 如需 [開啟原則 - <原則名稱>] 對話方塊可用之選項的詳細資訊，請參閱[建立新原則或開啟原則對話方塊，一般頁面](../../relational-databases/policy-based-management/create-new-policy-or-open-policy-dialog-box-general-page.md)和[建立新原則或開啟原則對話方塊，描述頁面](../../relational-databases/policy-based-management/create-new-policy-or-open-policy-dialog-box-description-page.md)。  
  
6.  完成後，請按一下 **[確定]**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-a-policys-properties"></a>若要檢視原則的屬性  
  
1.  在 **[物件總管]**中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    USE msdb;  
    GO  
    SELECT name,  
       execution_mode,  
       description,  
       is_enabled,  
       job_id  
    FROM syspolicy_policies;  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [syspolicy_policies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syspolicy-policies-transact-sql.md)。  
  
  
