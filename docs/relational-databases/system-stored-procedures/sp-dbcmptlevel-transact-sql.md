---
title: sp_dbcmptlevel (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbcmptlevel
- sp_dbcmptlevel_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbcmptlevel
ms.assetid: 508c686d-2bd4-41ba-8602-48ebca266659
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 96bd1aa87dba90963588db74935294c0dcdd8f0b
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58527421"
---
# <a name="spdbcmptlevel-transact-sql"></a>sp_dbcmptlevel (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  設定要相容於指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的資料庫行為。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 使用[ALTER DATABASE 相容性層級](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)改。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dbcmptlevel [ [ @dbname = ] name ]   
    [ , [ @new_cmptlevel = ] version ]  
```  
  
## <a name="arguments"></a>引數  
`[ @dbname = ] name` 是要變更相容性層級的資料庫名稱。 資料庫名稱必須符合識別碼的規則。 *名稱*已**sysname**，預設值是 NULL。  
  
`[ @new_cmptlevel = ] version` 是的新版[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]與資料庫所要相容。 *版本*已**tinyint**，預設值是 NULL。 此值必須是下列其中之一：  
  
 **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
  
 **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
 **110** = [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
 **120** = [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
 **130** = [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 如果未不指定任何參數，或如果*名稱*未指定參數， **sp_dbcmptlevel**會傳回錯誤。  
  
 如果*名稱*指定不含*版本*，則[!INCLUDE[ssDE](../../includes/ssde-md.md)]傳回訊息，顯示指定之資料庫的目前的相容性層級。  
  
## <a name="remarks"></a>備註  
 如需相容性層級的描述，請參閱 < [ALTER DATABASE 相容性層級&#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)。  
  
## <a name="permissions"></a>Permissions  
 只有資料庫擁有者、 隸屬**sysadmin**固定伺服器角色，而**db_owner**固定的資料庫角色 （如果您要變更目前的資料庫） 可以執行此程序。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [保留關鍵字 &#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
