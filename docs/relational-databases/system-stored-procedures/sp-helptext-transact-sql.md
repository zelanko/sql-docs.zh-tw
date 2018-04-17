---
title: sp_helptext (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helptext
- sp_helptext_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helptext
ms.assetid: 24135456-05f0-427c-884b-93cf38dd47a8
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ff9b4c0dd094cbe8e3a3816a1f0a8efd1dc64335
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sphelptext-transact-sql"></a>sp_helptext (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  顯示使用者自訂規則定義、預設值、未加密的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序、使用者自訂的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函數、觸發程序、計算資料行、CHECK 條件約束、檢視，或系統預存程序之類的系統物件。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helptext [ @objname = ] 'name' [ , [ @columnname = ] computed_column_name ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@objname =** ] **'***name***'**  
 這是使用者自訂、結構描述範圍物件的限定或非限定名稱。 只有在指定限定物件時，才會用到引號。 如果提供其中包括資料庫名稱的完整名稱，資料庫名稱就必須是目前資料庫的名稱。 這個物件必須在目前的資料庫中。 *名稱*是**nvarchar(776)**，沒有預設值。  
  
 [  **@columnname =** ] **'***computed_column_name***'**  
 這是要顯示定義資訊的計算資料行名稱。 包含資料行的資料表，必須指定為*名稱*。 *column_name*是**sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**文字**|**nvarchar(255)**|物件定義|  
  
## <a name="remarks"></a>備註  
 sp_helptext 會顯示在多個資料列中建立物件所用的定義。 每一個資料列都包含 255 個字元的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 定義。 這個定義位在**定義**中的資料行[sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)目錄檢視。  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色中的成員資格。 系統物件定義是公開顯示的。 凡具有 ALTER、CONTROL、TAKE OWNERSHIP 或 VIEW DEFINITION 任一權限的物件擁有者或被授與者，都看得到使用者物件的定義。  
  
## <a name="examples"></a>範例  
  
### <a name="a-displaying-the-definition-of-a-trigger"></a>A. 顯示觸發程序的定義  
 下列範例會顯示 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中 `dEmployee` 觸發程序的定義。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_helptext 'HumanResources.dEmployee';  
GO  
```  
  
### <a name="b-displaying-the-definition-of-a-computed-column"></a>B. 顯示計算資料行的定義  
 下列範例會顯示 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中的 `TotalDue` 資料表的計算資料行 `SalesOrderHeader` 的定義。  
  
```  
USE AdventureWorks2012;  
GO  
sp_helptext @objname = N'AdventureWorks2012.Sales.SalesOrderHeader', @columnname = TotalDue ;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Text`  
  
 `---------------------------------------------------------------------`  
  
 `(isnull(([SubTotal]+[TaxAmt])+[Freight],(0)))`  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
