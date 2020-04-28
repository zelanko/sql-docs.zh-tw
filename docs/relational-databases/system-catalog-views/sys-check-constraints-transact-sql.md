---
title: sys.databases check_constraints （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/28/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.check_constraints
- sys.check_constraints_TSQL
- check_constraints_TSQL
- check_constraints
dev_langs:
- TSQL
helpviewer_keywords:
- sys.check_constraints catalog view
ms.assetid: 940ebc5e-44ba-4dae-8b29-da94f2d1d6c4
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2212ebe8551f27c880ebf0c674f4b8d134617b07
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67942501"
---
# <a name="syscheck_constraints-transact-sql"></a>sys.check_constraints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對每個屬於 CHECK 條件約束的物件，各包含一個資料列，其為**sys.databases。類型**= ' C '。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**\<繼承自 sys.databases 的資料行>**||如需此視圖所繼承之資料行的清單，請參閱[sys.databases &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。|  
|**is_disabled**|**bit**|CHECK 條件約束已停用。|  
|**is_not_for_replication**|**bit**|CHECK 條件約束是利用 NOT FOR REPLICATION 選項來建立的。|  
|**is_not_trusted**|**bit**|不是所有資料列的 CHECK 條件約束都經過系統驗證過了。|  
|**parent_column_id**|**int**|0 表示資料表層級 CHECK 條件約束。<br /><br /> 非零值則表示這是在具有指定識別碼值之資料行定義的資料行層級 CHECK 條件約束。|  
|**definition**|**nvarchar(max)**|定義這個 CHECK 條件約束的 SQL 運算式。|  
|**uses_database_collation**|**bit**|1 = 條件約束定義須依據資料庫的預設定序進行正確評估；否則為 0。 這種相依性可以防止資料庫預設定序變更。|  
|**is_system_named**|**bit**|1 = 名稱是系統所產生。<br /><br /> 0 = 名稱是使用者所提供。|  
  
## <a name="permissions"></a>權限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的物件目錄檢視](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
