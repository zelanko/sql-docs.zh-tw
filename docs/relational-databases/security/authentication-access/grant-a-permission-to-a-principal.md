---
title: 為主體授與權限 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Grant permission to a principal
ms.assetid: 4107389d-05b6-4aa3-9fa8-95b40cdf05dc
caps.latest.revision: 12
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 599420f613d022470856bdb7d874aa0d3d3fcb66
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/18/2018
ms.locfileid: "39109660"
---
# <a name="grant-a-permission-to-a-principal"></a>為主體授與權限
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中為主體授與權限。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **若要使用下列項目為主體授與權限：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
 請考慮下列更輕鬆管理權限的最佳做法。  
  
-   將權限授與角色，而非個別登入或使用者。 當某位人員被另一位人員取代時，請從角色中移除離開的人員，並將新的人員加入至角色。 此時，許多可能與該角色相關聯的權限就會自動提供給新的人員使用。 如果組織中的許多人員需要相同的權限，只要將每位人員加入至角色，就會授與他們相同的權限。  
  
-   設定要由結構描述擁有的類似安全性實體 (資料表、檢視表和程序)，然後授與結構描述的權限。 例如，薪資結構描述可能會擁有許多資料表、檢視表和預存程序。 只要授與此結構描述的存取權，就可以同時授與執行薪資功能的所有必要權限。 如需有關哪些安全性實體可以被授與權限的詳細資訊，請參閱＜ [Securables](../../../relational-databases/security/securables.md)＞。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 同意授權者 (或是指定了 AS 選項的主體) 必須具有指定了 GRANT OPTION 的權限本身，或是具有隱含目前正在授與權限的更高權限。 **系統管理員 (sysadmin)** 固定伺服器角色的成員也能夠授與任何權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-grant-permission-to-a-principal"></a>若要為主體授與權限  
  
1.  在 [物件總管] 中，展開包含您要授與權限之物件的資料庫。  
  
    > [!NOTE]  
    >  這些步驟特別處理授與預存程序的權限，但是您可以使用類似步驟加入資料表、檢視、函數、組件，以及其他安全性實體的權限。 如需詳細資訊，請參閱 [GRANT &#40;Transact-SQL&#41;](../../../t-sql/statements/grant-transact-sql.md)  
  
2.  展開 **[可程式性]** 資料夾。  
  
3.  展開 **[預存程序]** 資料夾。  
  
4.  以滑鼠右鍵按一下預存程序，然後選取 [屬性]。  
  
5.  在 [預存程序屬性] - *stored_procedure_name>* 對話方塊的 [選取頁面] 底下，選取 [權限]。 使用此頁面將使用者或角色加入至預存程序，並指定這些使用者或角色擁有的權限。  
  
6.  完成後，請按一下 **[確定]**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-grant-permission-to-a-principal"></a>若要為主體授與權限  
  
1.  在 **[物件總管]** 中，連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。  
  
    ```  
    -- Grants EXECUTE permission on stored procedure HumanResources.uspUpdateEmployeeHireInfo to an application role called Recruiting11.   
    USE AdventureWorks2012;  
    GO  
    GRANT EXECUTE ON OBJECT::HumanResources.uspUpdateEmployeeHireInfo  
        TO Recruiting11;  
    GO  
    ```  
  
 如需詳細資訊，請參閱 [GRANT &#40;Transact-SQL&#41;](../../../t-sql/statements/grant-transact-sql.md) 和[授與物件權限 &#40;Transact-SQL&#41;](../../../t-sql/statements/grant-object-permissions-transact-sql.md)。  
  
## <a name="see-also"></a>另請參閱  
 [主體 &#40;Database Engine&#41;](../../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
