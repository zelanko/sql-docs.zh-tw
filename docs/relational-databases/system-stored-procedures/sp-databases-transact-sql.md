---
title: "sp_databases (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_databases_TSQL
- sp_databases
dev_langs: TSQL
helpviewer_keywords: sp_databases
ms.assetid: 2a83b92a-9ecc-43c4-8ff4-e91e3a940b5a
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b6133cef4500d7066f38a51f5a5f124d1e879e01
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2017
---
# <a name="spdatabases-transact-sql"></a>sp_databases (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列出在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中的資料庫，或可利用資料庫閘道來存取的資料庫。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_databases  
```  
  
## <a name="return-code-values"></a>傳回碼值  
 無  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**資料庫名稱**|**sysname**|資料庫的名稱。 在[!INCLUDE[ssDE](../../includes/ssde-md.md)]，這個資料行代表資料庫名稱中所儲存**sys.databases**目錄檢視。|  
|**DATABASE_SIZE**|**int**|資料庫的大小 (以 KB 為單位)。|  
|**註解**|**varchar(254)**|對於 [!INCLUDE[ssDE](../../includes/ssde-md.md)]，這個欄位一律會傳回 NULL。|  
  
## <a name="remarks"></a>備註  
 傳回的資料庫名稱可用來作為 USE 陳述式中的參數，以變更目前資料庫的內容。  
  
 **sp_databases**開放式資料庫連接 (ODBC) 中已沒有對等項目。  
  
## <a name="permissions"></a>Permissions  
 需要 CREATE DATABASE、ALTER ANY DATABASE 或 VIEW ANY DEFINITION 權限，且必須擁有資料庫的存取權限。 無法拒絕 VIEW ANY DEFINITION 權限。  
  
## <a name="examples"></a>範例  
 下列範例會顯示如何執行 `sp_databases`。  
  
```tsql  
USE master;  
GO  
EXEC sp_databases;  
```  
  
## <a name="see-also"></a>請參閱  
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [HAS_DBACCESS &#40;TRANSACT-SQL &#41;](../../t-sql/functions/has-dbaccess-transact-sql.md)  
  
  
