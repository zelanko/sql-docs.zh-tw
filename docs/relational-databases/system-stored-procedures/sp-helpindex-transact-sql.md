---
description: sp_helpindex (Transact-SQL)
title: sp_helpindex (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpindex_TSQL
- sp_helpindex
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpindex
ms.assetid: c7f73ba0-ec35-4b10-aa5f-f1487e51fbf7
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a011e8f19650dad1c52b4a88e81edf28eb0bfc47
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97462689"
---
# <a name="sp_helpindex-transact-sql"></a>sp_helpindex (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  報告資料表或檢視之索引的相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpindex [ @objname = ] 'name'  
```  
  
## <a name="arguments"></a>引數  
`[ @objname = ] 'name'` 這是使用者定義資料表或視圖的限定或非限定名稱。 只有在指定完整資料表或檢視表名稱時，才會用到引號。 如果提供其中包括資料庫名稱的完整名稱，資料庫名稱就必須是目前資料庫的名稱。 *名稱* 是 **Nvarchar (776)**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**index_name**|**sysname**|索引名稱。|  
|**index_description**|**Varchar (210)**|索引描述，其中包括所在的檔案群組。|  
|**index_keys**|**Nvarchar (2078)**|建立索引的資料表或檢視資料行。|  
  
 遞減索引資料行會列在結果集中，名稱後面會有一個減號 (-)；預設值是遞增索引資料行，會單獨列出名稱。  
  
## <a name="remarks"></a>備註  
 如果已使用 UPDATE STATISTICS 的 NORECOMPUTE 選項來設定索引，該資訊就會包含在 **index_description** 資料行中。  
  
 **sp_helpindex** 只會公開能排序的索引資料行;因此，它不會公開 XML 索引或空間索引的相關資訊。  
  
## <a name="permissions"></a>權限  
 需要 **public** 角色的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會報告 `Customer` 資料表的索引類型。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_helpindex N'Sales.Customer';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的資料庫引擎預存程式 ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)  
  
  
