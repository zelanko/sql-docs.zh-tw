---
title: sys.systypes & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.systypes_TSQL
- systypes_TSQL
- sys.systypes
- systypes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.systypes compatibility view
- systypes system table
ms.assetid: 1b0b1d0c-5f7b-470b-bd52-8bfa922d7889
caps.latest.revision: 50
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 32f3ff7bb65822e0ce0c8e3e9192b88dd572c22b
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39537218"
---
# <a name="syssystypes-transact-sql"></a>sys.systypes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  針對資料庫中所定義的每個系統提供資料類型和每個使用者自訂資料類型，各傳回一個資料列。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|資料類型名稱。|  
|**xtype**|**tinyint**|實體儲存類型。|  
|**status**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xusertype**|**smallint**|擴充使用者類型。 如果資料類型的數目超過 32,767，則會造成溢位或傳回 NULL。|  
|**長度**|**smallint**|資料類型的實際長度。|  
|**xprec**|**tinyint**|符合伺服器所用的內部有效位數。 不會用在查詢中。|  
|**xscale**|**tinyint**|符合伺服器所用的內部小數位數。 不會用在查詢中。|  
|**tdefault**|**int**|包含這個資料類型之完整性檢查的預存處理序識別碼。|  
|**網域**|**int**|包含這個資料類型之完整性檢查的預存處理序識別碼。|  
|**uid**|**smallint**|類型擁有者的結構描述識別碼。<br /><br /> 如果是從舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升級而來的資料庫，結構描述識別碼會等於擁有者的使用者識別碼。<br /><br /> **\*\* 重要\* \* **如果您使用下列任一項[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DDL 陳述式中，您必須使用[sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)目錄檢視，而不是**sys.systypes**。<br /><br /> ALTER AUTHORIZATION ON TYPE<br /><br /> CREATE TYPE<br /><br /> 如果使用者和角色數目超過 32,767 個，則會造成溢位或傳回 NULL。|  
|**保留**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**collationid**|**int**|字元為基礎，如果**collationid**是目前資料庫的定序識別碼，否則它便是 NULL。|  
|**usertype**|**smallint**|使用者類型識別碼。 如果資料類型的數目超過 32,767，則會造成溢位或傳回 NULL。|  
|**variable**|**bit**|可變長度資料類型。<br /><br /> 1 = True<br /><br /> 0 = False|  
|**allownulls**|**bit**|指出這項資料類型的預設 Null 屬性。 此預設值會覆寫如果藉由指定 null 屬性[CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)或是[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)。|  
|**type**|**tinyint**|實體儲存體資料類型。|  
|**printfmt**|**varchar(255)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**prec**|**smallint**|這個資料類型的有效位數層級。<br /><br /> -1 = **xml**或大數值類型。|  
|**scale**|**tinyint**|這個資料類型的小數位數 (以有效位數為基礎)。<br /><br /> NULL = 資料類型是非數值。|  
|**定序**|**sysname**|字元為基礎，如果**定序**是定序的目前資料庫中; 否則它便是 NULL。|  
  
## <a name="see-also"></a>另請參閱  
 [相容性檢視&#40;Transact SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)   
 [將系統資料表對應至系統檢視表&#40;Transact SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)  
  
  
