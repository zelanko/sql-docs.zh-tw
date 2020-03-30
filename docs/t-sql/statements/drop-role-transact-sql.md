---
title: DROP ROLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/11/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP ROLE
- DROP_ROLE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting roles
- database roles [SQL Server], removing
- removing roles
- DROP ROLE statement
- roles [SQL Server], removing
- dropping roles
ms.assetid: 1f6f13ae-56a2-4ef1-93f5-8e6151b83e1d
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3b3227fa8aa15b2254e6f4a38caa0e5ac60163a7
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "68043924"
---
# <a name="drop-role-transact-sql"></a>DROP ROLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  從資料庫中移除角色。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server  
  
DROP ROLE [ IF EXISTS ] role_name  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DROP ROLE role_name  
```  
  
## <a name="arguments"></a>引數  
 *IF EXISTS*  
 **適用於**：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至[目前版本](https://go.microsoft.com/fwlink/p/?LinkId=299658))。  
  
 只有在角色已存在時，才能有條件地將其卸除。  
  
 *role_name*  
 指定要從資料庫卸除的角色。  
  
## <a name="remarks"></a>備註  
 擁有安全性實體的角色，不可以從資料庫卸除。 若要卸除一個擁有安全性實體的資料庫角色，必須先傳送那些安全性實體的擁有權，或者從資料庫卸除它們。 含有成員的角色，不可以從資料庫卸除。 若要卸除一個含有成員的角色，必須先移除該角色的成員。  
  
 若要從資料庫角色中移除成員，請使用 [ALTER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-role-transact-sql.md)。  
  
 您不可以利用 DROP ROLE 來卸除固定資料庫角色。  
  
 您可以在 sys.database_role_members 目錄檢視中，檢視角色成員資格的相關資訊。  
  
> [!CAUTION]  
>  [!INCLUDE[ssCautionUserSchema](../../includes/sscautionuserschema-md.md)]  
  
 若要移除伺服器角色，請使用 [DROP SERVER ROLE & #40;TRANSACT-SQL & #41;](../../t-sql/statements/drop-server-role-transact-sql.md)。  
  
## <a name="permissions"></a>權限  
 需要資料庫的 **ALTER ANY ROLE** 權限、角色的 **CONTROL** 權限，或 **db_securityadmin** 的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會從 `purchasing` 資料庫卸除資料庫角色 `AdventureWorks2012`。  
  
```  
DROP ROLE purchasing;  
GO  
```  
  
  
## <a name="see-also"></a>另請參閱  
 [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [ALTER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-role-transact-sql.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sys.database_role_members &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [安全性函數 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  


