---
title: DATABASE_PRINCIPAL_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DATABASE_PRINCIPAL_ID_TSQL
- DATABASE_PRINCIPAL_ID
dev_langs:
- TSQL
helpviewer_keywords:
- identification numbers [SQL Server], principals
- principal ID numbers [SQL Server]
- DATABASE_PRINCIPAL_ID function
- IDs [SQL Server], principals
ms.assetid: 908c7dd8-c10b-4658-92f6-0224f9835dd9
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: e0583570ce9a4d11b2e4aa6c019c8f4ccc753239
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="databaseprincipalid-transact-sql"></a>DATABASE_PRINCIPAL_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

包傳回目前資料庫中的主體識別碼。 如需主體的詳細資訊，請參閱[主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DATABASE_PRINCIPAL_ID ( 'principal_name' )  
```  
  
## <a name="arguments"></a>引數  
*principal_name*  
為代表主體，類型為 **sysname** 的運算式。  
若省略 *principal_name*，則會傳回目前使用者的識別碼。 它必須用括號括住。
  
## <a name="return-types"></a>傳回類型
**int**  
當資料庫主體不存在時為 NULL。
  
## <a name="remarks"></a>Remarks  
DATABASE_PRINCIPAL_ID 可以用在選取清單、WHERE 子句或運算式所允許的任何位置。 如需詳細資訊，請參閱[運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)。
  
## <a name="examples"></a>範例  
  
### <a name="a-retrieving-the-id-of-the-current-user"></a>A. 擷取目前使用者的識別碼  
下列範例會傳回目前使用者的資料庫主體識別碼。
  
```sql
SELECT DATABASE_PRINCIPAL_ID();  
GO  
```  
  
### <a name="b-retrieving-the-id-of-a-specified-database-principal"></a>B. 擷取指定資料庫主體的識別碼  
下列範例會傳回資料庫角色 `db_owner` 的資料庫主體識別碼。
  
```sql
SELECT DATABASE_PRINCIPAL_ID('db_owner');  
GO  
```  
  
## <a name="see-also"></a>另請參閱
[主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
[權限階層 &#40;Database Engine&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)  
[sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)
  
  
