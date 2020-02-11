---
title: sp_helpstats （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpstats
- sp_helpstats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpstats
ms.assetid: 00ab3cfd-2736-4fc0-b1b2-16dd49fb2fe5
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fba09255204b796a5134e8b8098e650430b7de63
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68048400"
---
# <a name="sp_helpstats-transact-sql"></a>sp_helpstats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回指定資料表之資料行和索引的統計資料資訊。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]若要取得有關統計資料的資訊，請查詢[sys.databases](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)和[sys.databases stats_columns](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)目錄 views。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpstats[ @objname = ] 'object_name'   
     [ , [ @results = ] 'value' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @objname = ] 'object_name'`指定要提供統計資料資訊的資料表。 *object_name*是**Nvarchar （520）** ，而且不可以是 null。 可以指定一部分名稱或兩部分名稱。  
  
`[ @results = ] 'value'`指定要提供的資訊範圍。 有效的專案包括 [**全部**] 和 [**統計**資料]。 **All**會列出所有索引的統計資料，以及已在其上建立統計資料的資料行;**STATS**只會列出與索引沒有關聯的統計資料。 *value*是**Nvarchar （5）** ，預設值是 STATS。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 下表描述結果集中的資料行。  
  
|資料行名稱|描述|  
|-----------------|-----------------|  
|**statistics_name**|統計資料的名稱。 傳回**sysname** ，而且不可以是 null。|  
|**statistics_keys**|統計資料的基礎索引鍵。 傳回**Nvarchar （2078）** ，而且不可以是 null。|  
  
## <a name="remarks"></a>備註  
 請利用 DBCC SHOW_STATISTICS 來顯示任何特定索引或統計資料的詳細統計資訊。 如需詳細資訊，請參閱[DBCC SHOW_STATISTICS &#40;transact-sql&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)和[sp_helpindex &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md)。  
  
## <a name="permissions"></a>權限  
 需要 **public** 角色的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會執行 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 來建立 `sp_createstats` 資料庫中所有使用者資料表之所有適用資料行的單一資料行統計資料。 之後，便會執行 `sp_helpstats` 來尋找在 `Customer` 資料表上建立的結果統計資料。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_createstats;  
GO  
EXEC sp_helpstats   
@objname = 'Sales.Customer',  
@results = 'ALL';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `statistics_name               statistics_keys`  
  
 `----------------------------  ----------------`  
  
 `_WA_Sys_00000003_22AA2996     AccountNumber`  
  
 `AK_Customer_AccountNumber     AccountNumber`  
  
 `AK_Customer_rowguid           rowguid`  
  
 `CustomerType                  CustomerType`  
  
 `IX_Customer_TerritoryID       TerritoryID`  
  
 `ModifiedDate                  ModifiedDate`  
  
 `PK_Customer_CustomerID        CustomerID`  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [資料庫引擎預存程式 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
