---
title: 設定原則式管理的一般屬性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.dmf.PolicyManagement.f1
helpviewer_keywords:
- Policy-Based Management, configure properties
ms.assetid: 6d1e0e37-29ea-408a-a055-384984d884be
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 249b338148dc762e091d0be47bc081fe87c72fcd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63162390"
---
# <a name="configure-the-general-properties-of-policy-based-management"></a>設定原則式管理的一般屬性
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中設定原則式管理的屬性。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目設定原則式管理：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要 PolicyAdministratorRole 固定資料庫角色中的成員資格。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-configure-policy-based-management"></a>設定以原則為基礎的管理  
  
1.  在物件總管**** 中，按一下加號，展開您想要設定原則式管理屬性的伺服器。  
  
2.  按一下加號展開 **[管理]** 資料夾。  
  
3.  以滑鼠右鍵按一下 [原則管理]****，然後選取 [屬性]****。  
  
     **[原則管理屬性]** 對話方塊有下列選項。  
  
     **已啟用**  
     指定是否啟用以原則為基礎的管理。  
  
     **HistoryRetentionInDays**  
     指定原則評估記錄應保留的天數。 如果這個值為 0 (預設值)，將不會自動移除記錄。  
  
     **LogOnSuccess**  
     指定以原則為基礎的管理是否會記錄成功的原則評估。  
  
    -   當這個值為 false (預設值) 時，只會記錄失敗的原則評估。  
  
    -   當這個值為 true 時，成功和失敗的原則評估都會記錄下來。  
  
4.  完成時按一下 **[確定]**。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-configure-policy-based-management"></a>設定以原則為基礎的管理  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。  
  
    ```  
    -- enables Policy-Based Management   
    USE msdb;  
    GO  
    EXEC dbo.sp_syspolicy_configure   
         @name = N'Enabled',   
         @value = 1;  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [sp_syspolicy_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syspolicy-configure-transact-sql)。  
  
  
