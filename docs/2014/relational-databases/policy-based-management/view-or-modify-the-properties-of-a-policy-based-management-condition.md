---
title: 檢視或修改原則式管理條件的屬性 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Policy-Based Management, view policy conditions
- Policy-Based Management, modify policy conditions
ms.assetid: 890d7384-8444-4767-bb6f-f5debb155747
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3d45f6a3a5fc4c5f139808778758d3d3c0cc1da7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030502"
---
# <a name="view-or-modify-the-properties-of-a-policy-based-management-condition"></a>檢視或修改原則式管理條件的屬性
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中檢視或修改原則式管理條件的屬性。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [Security](#Security)  
  
-   **若要檢視或修改條件的屬性，請使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 需要 msdb 資料庫中 PolicyAdministratorRole 角色的成員資格。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-or-modify-a-conditions-properties"></a>若要檢視或修改條件的屬性  
  
1.  在 **[物件總管]** 中，按一下加號，展開包含您想要檢視或修改之條件的伺服器。  
  
2.  按一下加號展開 **[管理]** 資料夾。  
  
3.  按一下加號展開 **[原則管理]**。  
  
4.  按一下加號展開 **[條件]** 資料夾。  
  
5.  以滑鼠右鍵按一下您想要檢視或編輯的條件，然後選取 [屬性]。 如需 [開啟條件 - <條件名稱>] 對話方塊可用之選項的詳細資訊，請參閱[建立新條件或開啟條件對話方塊，一般頁面](../../integration-services/general-page-of-integration-services-designers-options.md)、[開啟條件對話方塊，相依原則頁面](open-condition-dialog-box-dependent-policies-page.md)、[建立新條件或開啟條件對話方塊，描述頁面](create-new-condition-or-open-condition-dialog-box-description-page.md)和[進階編輯 &#40;條件&#41; 對話方塊](advanced-edit-condition-dialog-box.md)。  
  
6.  完成後，請按一下 **[確定]**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-a-conditions-properties"></a>若要檢視條件的屬性  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    USE msdb;  
    GO  
    SELECT name,  
       description,  
       facet,  
       expression,  
       is_name_condition,  
       obj_name  
    FROM syspolicy_conditions;  
    GO  
  
    ```  
  
 如需詳細資訊，請參閱 [syspolicy_conditions &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/syspolicy-conditions-transact-sql)。  
  
  
