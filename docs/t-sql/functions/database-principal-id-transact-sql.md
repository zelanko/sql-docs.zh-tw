---
title: "DATABASE_PRINCIPAL_ID (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0a26dcac49e19f9a0dda738e58042c83cb8e46b8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="databaseprincipalid-transact-sql"></a>DATABASE_PRINCIPAL_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

包傳回目前資料庫中的主體識別碼。 如需有關主體的詳細資訊，請參閱[主體 &#40; Database engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DATABASE_PRINCIPAL_ID ( 'principal_name' )  
```  
  
## <a name="arguments"></a>引數  
*principal_name*  
這是類型的運算式**sysname**代表主體之。  
當*principal_name*已省略，則會傳回目前使用者的識別碼。 它必須用括號括住。
  
## <a name="return-types"></a>傳回型別
**int**  
當資料庫主體不存在時為 NULL。
  
## <a name="remarks"></a>備註  
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
  
  

