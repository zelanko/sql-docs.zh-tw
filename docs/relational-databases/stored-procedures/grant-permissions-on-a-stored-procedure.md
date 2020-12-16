---
title: 授與預存程序的權限 | Microsoft Docs
description: 了解如何使用 SQL Server Management Studio 或 Transact-SQL 在 SQL Server 2019 (15.x) 中授與預存程序的權限。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [SQL Server], permissions
ms.assetid: a7d15816-a788-4099-ad91-dc4b26618299
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b7a5b7631a2c3122bc97a2c93c9d6c0ae202bb04
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475279"
---
# <a name="grant-permissions-on-a-stored-procedure"></a>授與預存程序的權限
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中授與預存程序的權限。 權限可以授與資料庫中現有的使用者、資料庫角色或應用程式角色。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [安全性](#Security)  
  
-   **使用下列方法授與預存程序的權限：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   您無法使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 授與系統程序或系統函數的權限。 請改用 [GRANT 物件權限](../../t-sql/statements/grant-object-permissions-transact-sql.md) 。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 同意授權者 (或是指定了 AS 選項的主體) 必須具有指定了 GRANT OPTION 的權限本身，或是具有隱含目前正在授與權限的更高權限。 需要程序所屬結構描述的 ALTER 權限，或程序的 CONTROL 權限。 如需詳細資訊，請參閱 [GRANT 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)中授與預存程序的權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-grant-permissions-on-a-stored-procedure"></a>若要授與預存程序的權限  
  
1.  在物件總管中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，然後展開該執行個體。  
  
2.  依序展開 **[資料庫]** 、程序所屬的資料庫，以及 **[可程式性]** 。  
  
3.  展開 [預存程序]，以滑鼠右鍵按一下要授與權限的程序，然後按一下 [屬性]。  
  
4.  在 **[預存程序屬性]** 上選取 **[權限]** 頁面。  
  
5.  若要將權限授與使用者、資料庫角色或應用程式角色，請按一下 **[搜尋]** 。  
  
6.  在 **[選取使用者或角色]** 中，按一下 **[物件類型]** ，以加入或清除想要的使用者和角色。  
  
7.  按一下 **[瀏覽]** 顯示使用者或角色的清單。 選取要獲得權限授與的使用者或角色。  
  
8.  在 **[明確權限]** 方格中，選取要授與指定使用者或角色的權限。 如需權限的說明，請參閱 [權限 &#40;Database Engine&#41;](../../relational-databases/security/permissions-database-engine.md)。  

 選取 **[授與]** 表示要將指定的權限提供給被授與者。 選取 **[可授與]** 則表示授與者也能夠將指定的權限授與給其他主體。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-grant-permissions-on-a-stored-procedure"></a>若要授與預存程序的權限  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 此範例會將預存程序 `EXECUTE` 的 `HumanResources.uspUpdateEmployeeHireInfo` 權限授與名為 `Recruiting11`的應用程式角色。  
  
```sql  
USE AdventureWorks2012;   
GRANT EXECUTE ON OBJECT::HumanResources.uspUpdateEmployeeHireInfo  
    TO Recruiting11;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [GRANT 物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)   
 [建立預存程序](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [修改預存程序](../../relational-databases/stored-procedures/modify-a-stored-procedure.md)   
 [刪除預存程序](../../relational-databases/stored-procedures/delete-a-stored-procedure.md)   
 [重新命名預存程序](../../relational-databases/stored-procedures/rename-a-stored-procedure.md)  
  
  
