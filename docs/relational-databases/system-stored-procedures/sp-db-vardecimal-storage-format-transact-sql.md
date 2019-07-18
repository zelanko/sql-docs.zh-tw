---
title: sp_db_vardecimal_storage_format (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_db_vardecimal_storage_format
- sp_db_vardecimal_storage_format_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_db_vardecimal_storage_format
- decimal data type, compressing
- compressing decimal data
- numeric data type, compressing
- database compression [SQL Server]
- table compression [SQL Server]
ms.assetid: 9920b2f7-b802-4003-913c-978c17ae4542
author: stevestein
ms.author: sstein
ms.openlocfilehash: 28628ee5dc8ff1bde7906dfea7fca60470720e11
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108218"
---
# <a name="spdbvardecimalstorageformat-transact-sql"></a>sp_db_vardecimal_storage_format (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回資料庫目前的 Vardecimal 儲存格式狀態，或是啟用 Vardecimal 儲存格式的資料庫。  從 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 開始，一定會啟用使用者資料庫。 只有在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中才需要啟用 Vardecimal 儲存格式的資料庫。  
  
> [!IMPORTANT]  
>  變更資料庫的 Vardecimal 儲存格式狀態可能會影響備份和復原、資料庫鏡像、sp_attach_db、記錄傳送和複寫。  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_db_vardecimal_storage_format [ [ @dbname = ] 'database_name']   
    [ , [ @vardecimal_storage_format = ] { 'ON' | 'OFF' } ]   
[;]  
```  
  
## <a name="arguments"></a>引數  
 [ @dbname= ] '*database_name*'  
 這是即將變更儲存格式之資料庫的名稱。 *database_name*已**sysname**，沒有預設值。 如果省略資料庫名稱，就會傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中所有資料庫的 Vardecimal 儲存格式狀態。  
  
 [ @vardecimal_storage_format=] {'ON' |'關閉 '}  
 指定是否啟用 Vardecimal 儲存格式。 @vardecimal_storage_format 可以是 ON 或 OFF。 參數是**varchar(3)** ，沒有預設值。 如果提供了資料庫名稱，但省略 @vardecimal_storage_format，就會傳回指定之資料庫的目前設定。 這個引數對於 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更新版本沒有任何作用。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 如果無法變更資料庫儲存格式，sp_db_vardecimal_storage_format 就會傳回錯誤。 如果資料庫已經處於指定的狀態，此預存程序就沒有任何作用。  
  
 如果@vardecimal_storage_format未提供引數，則會傳回資料庫名稱和 Vardecimal State 資料行。  
  
## <a name="remarks"></a>備註  
 sp_db_vardecimal_storage_format 會傳回 Vardecimal 狀態，但是無法變更 Vardecimal 狀態。  
  
 在下列情況中，sp_db_vardecimal_storage_format 將會失敗：  
  
-   資料庫中存在使用中使用者。  
  
-   資料庫已啟用鏡像。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的版本不支援 Vardecimal 儲存格式。  
  
 若要將 Vardecimal 儲存格式狀態變更為 OFF，資料庫就必須設定為簡單復原模式。 當資料庫設定為簡單復原模式時，就會中斷記錄鏈結。 在您將 Vardecimal 儲存格式狀態設定為 OFF 之後，請執行完整資料庫備份。  
  
 如果有資料表正使用 Vardecimal 資料庫壓縮，將此狀態變更為 OFF 將會失敗。 若要變更資料表的儲存格式，請使用[sp_tableoption](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)。 若要判斷資料庫中的哪個資料表正在使用 Vardecimal 儲存格式，請使用 `OBJECTPROPERTY` 函數並搜尋 `TableHasVarDecimalStorageFormat` 屬性，如下列範例所示。  
  
```  
USE AdventureWorks2012 ;  
GO  
SELECT name, object_id, type_desc  
FROM sys.objects   
 WHERE OBJECTPROPERTY(object_id,   
   N'TableHasVarDecimalStorageFormat') = 1 ;  
GO  
```  
  
## <a name="examples"></a>範例  
 下列程式碼會在 `AdventureWorks2012` 資料庫中啟用壓縮、確認狀態，然後壓縮 `Sales.SalesOrderDetail` 資料表中的十進位和數值資料行。  
  
```  
USE master ;  
GO  
  
EXEC sp_db_vardecimal_storage_format 'AdventureWorks2012', 'ON' ;  
GO  
  
-- Check the vardecimal storage format state for  
-- all databases in the instance.  
EXEC sp_db_vardecimal_storage_format ;  
GO  
  
USE AdventureWorks2012 ;  
GO  
  
EXEC sp_tableoption 'Sales.SalesOrderDetail', 'vardecimal storage format', 1 ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
