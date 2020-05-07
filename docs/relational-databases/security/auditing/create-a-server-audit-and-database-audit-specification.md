---
title: 建立伺服器稽核和資料庫稽核規格
description: 了解如何使用 SQL Server Management Studio 或 Transact-SQL (T-SQL) 來建立 SQL Server 稽核和資料庫稽核規格。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.sqlaudit.dbaudit.general.f1
helpviewer_keywords:
- audits [SQL Server], creating database specification
- database audit [SQL Server]
ms.assetid: 26ee85de-6e97-4318-b526-900924d96e62
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 55b848cd43e157a9a75670a24aea645c3279f7ea
ms.sourcegitcommit: bfb5e79586fd08d8e48e9df0e9c76d1f6c2004e9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/29/2020
ms.locfileid: "82262072"
---
# <a name="create-a-server-audit-and-database-audit-specification"></a>建立伺服器稽核和資料庫稽核規格
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本文描述如何使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../../includes/tsql-md.md)]，在 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 中建立伺服器稽核和資料庫稽核規格。  
  
 稽核 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫的執行個體牽涉到追蹤和記錄系統上所發生事件。 *SQL Server Audit* 物件會收集所要監視伺服器層級或資料庫層級動作和動作群組的單一執行個體。 此稽核位於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體層級。 您可以針對每個 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體設有多個稽核。 「資料庫層級稽核規格」  物件屬於稽核。 您可以針對每個稽核的每個 SQL Server 資料庫建立一個資料庫稽核規格。 如需詳細資訊，請參閱 [SQL Server Audit &#40;Database Engine&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md)。  
  
 ##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
 資料庫稽核規格是位於給定資料庫內的非安全性實體物件。 資料庫稽核規格在建立之後就會處於停用狀態。  
  
 當在使用者資料庫中建立或修改資料庫稽核規格時，請勿在伺服器範圍的物件 (例如系統檢視) 上包含稽核動作。 如果您包含伺服器範圍的物件，則會建立稽核。 但是，將不會包含伺服器範圍的物件，也不會傳回任何錯誤。 若要稽核伺服器範圍的物件，請在 master 資料庫中使用資料庫稽核規格。  
  
 資料庫稽核規格位於其建立所在的資料庫，但是 **TempDB** 系統資料庫除外。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
  
-   具有 ALTER ANY DATABASE AUDIT 權限的使用者可以建立資料庫稽核規格，並將其繫結至任何稽核。  
  
-   在建立資料庫稽核規格之後，具有 CONTROL SERVER 或 ALTER ANY DATABASE AUDIT 權限的主體可以檢視此規格。 系統管理員 (sysadmin) 帳戶也可以加以檢視。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-create-a-server-audit"></a>若要建立伺服器稽核  
  
1.  在 [物件總管] 中，展開 **[安全性]** 資料夾。  
  
2.  以滑鼠右鍵按一下 [稽核]  資料夾，然後選取 [新增稽核]  。 如需詳細資訊，請參閱[建立伺服器稽核與伺服器稽核規格](../../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)。  
  
3.  當完成選取選項時，請選取 [確定]  。  

#### <a name="to-create-a-database-level-audit-specification"></a>若要建立資料庫層級的稽核規格  
  
1.  在 [物件總管] 中，展開您要建立稽核規格的資料庫。  
  
2.  展開 **[安全性]** 資料夾。  
  
3.  以滑鼠右鍵按一下 [資料庫稽核規格]  資料夾，然後選取 [新增資料庫稽核規格]  。  
  
     [建立資料庫稽核規格]  對話方塊有下列選項：  
  
     **名稱**  
     資料庫稽核規格的名稱。 當建立伺服器稽核規格時，系統會自動產生名稱。 此名稱是可編輯的。  
  
     **稽核**  
     現有伺服器稽核物件的名稱。 請輸入稽核名稱或從清單中選取。  
  
     **稽核動作類型**  
     指定要擷取之資料庫層級的稽核動作群組和稽核動作。 如需資料庫層級稽核動作群組與稽核動作的清單及其所包含事件描述，請參閱 [SQL Server Audit 動作群組和動作](../../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md)。  
  
     **物件結構描述**  
     顯示指定之 [物件名稱]  的結構描述。  
  
     **Object Name**  
     要稽核的物件名稱。 此選項僅適用於稽核動作。 其不適用於稽核群組。  
  
     **省略符號 (...)**  
     開啟 [選取物件]  對話方塊，如此即可根據指定的 [稽核動作類型]  來瀏覽及選取可用物件。  
  
     **主體名稱**  
     依據所稽核的物件來篩選稽核的帳戶。  
  
     **省略符號 (...)**  
     開啟 [選取物件]  對話方塊，如此即可根據指定的 [物件名稱]  來瀏覽及選取可用物件。  
  
4.  當完成選取選項時，請選取 [確定]  。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-create-a-server-audit"></a>若要建立伺服器稽核  
  
1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，選取 [新增查詢]  。  
  
3.  將下列範例貼入查詢視窗中，然後選取 [執行]  。  
  
    ```  
    USE master ;  
    GO  
    -- Create the server audit.   
    CREATE SERVER AUDIT Payrole_Security_Audit  
        TO FILE ( FILEPATH =   
    'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA' ) ;   
    GO  
    -- Enable the server audit.   
    ALTER SERVER AUDIT Payrole_Security_Audit   
    WITH (STATE = ON) ;  
    ```  
  
#### <a name="to-create-a-database-level-audit-specification"></a>若要建立資料庫層級的稽核規格  
  
1.  在 [物件總管] 中，連接到 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]的執行個體。  
  
2.  在標準列上，選取 [新增查詢]  。  
  
3.  將下列範例貼入查詢視窗中，然後選取 [執行]  。 此範例會建立一個稱為 `Audit_Pay_Tables` 的資料庫稽核規格。 其可根據上一節中定義的伺服器稽核，針對 `HumanResources.EmployeePayHistory` 資料表以依照 `dbo` 使用者來稽核 SELECT 和 INSERT 陳述式。  
  
    ```  
    USE AdventureWorks2012 ;   
    GO  
    -- Create the database audit specification.   
    CREATE DATABASE AUDIT SPECIFICATION Audit_Pay_Tables  
    FOR SERVER AUDIT Payrole_Security_Audit  
    ADD (SELECT , INSERT  
         ON HumanResources.EmployeePayHistory BY dbo )   
    WITH (STATE = ON) ;   
    GO  
  
    ```  
  
 如需詳細資訊，請參閱 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-audit-transact-sql.md) 和 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-audit-specification-transact-sql.md)。  
  
  
