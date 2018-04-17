---
title: H (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- IHsyscolumns
- IHsyscolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHsyscolumns view
ms.assetid: 263452f1-9708-48f0-9536-402a89e7f5bf
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3860a82146f8fb9a91ac5d1a550d12d5c5e2a154
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="ihsyscolumns-transact-sql"></a>IHsyscolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHsyscolumns**檢視會公開發行來自非 SQL Server 發行者之發行項的資料行資訊。 這份檢視儲存在散發資料庫中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|資料行或程序參數的名稱。|  
|**id**|**int**|這個資料行所屬資料表的物件識別碼，或這個參數相關聯預存程序的識別碼。|  
|**xtype**|**tinyint**|從實體儲存體類型[sys.systypes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md)。|  
|**typestat**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xusertype**|**tinyint**|擴充使用者自訂資料類型的識別碼。|  
|**長度**|**bigint**|從最大實體儲存體長度[sys.systypes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md)。|  
|**xprec**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xscale**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colid**|**int**|資料行或參數識別碼。|  
|**xoffset**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**bitpos**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**保留**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colstat**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**cdefault**|**int**|這個資料行之預設值的識別碼。|  
|**網域**|**int**|這個資料行的規則或 CHECK 條件約束的識別碼。|  
|**number**|**int**|子程序數目的程序分組時 (**0**非程序項目)。|  
|**colorder**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**autoval**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**offset**|**int**|這個資料行出現在其中的資料列內位移。|  
|**collationid**|**int**|資料行定序的識別碼。 以非字元為基礎的資料行是 NULL。|  
|**語言**|**int**|資料行的語言識別碼。|  
|**status**|**int**|用來描述資料行或參數屬性的點陣圖：<br /><br /> **0x08** = 資料行允許 null 值。<br /><br /> **0x10** = ANSI 填補生效時**varchar**或**varbinary**加入資料行。 保留尾端空白**varchar**保留尾端零**varbinary**資料行。<br /><br /> **0x40** = 參數是輸出參數。<br /><br /> **0x80** = 資料行是識別資料行。|  
|**type**|**int**|從實體儲存體類型[sys.systypes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md)。|  
|**usertype**|**tinyint**|從使用者定義資料類型的識別碼[sys.systypes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md)。|  
|**printfmt**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**prec**|**int**|這個資料行的有效位數層級。|  
|**scale**|**int**|這個資料行的小數位數。|  
|**iscomputed**|**int**|這是一個旗標，指出這個資料行是否為計算資料行：<br /><br /> **0** = 非計算。<br /><br /> **1** = 計算。|  
|**isoutparam**|**int**|指出程序參數是否為輸出參數：<br /><br /> **1** = true。<br /><br /> **0** = false。|  
|**isnullable**|**int**|指出資料行是否允許 Null 值：<br /><br /> **1** = true。<br /><br /> **0** = false。|  
|**定序**|**int**|資料行的定序名稱。 以非字元為基礎的資料行是 NULL。|  
|**tdscollation**|**int**|當在表格式資料流 (TDS) 中傳回時，資料行的定序名稱。|  
  
## <a name="see-also"></a>另請參閱  
 [異質資料庫複寫](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視&#40;Transact SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
  
