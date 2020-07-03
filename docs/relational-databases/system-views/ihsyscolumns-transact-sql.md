---
title: IHsyscolumns （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHsyscolumns
- IHsyscolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHsyscolumns view
ms.assetid: 263452f1-9708-48f0-9536-402a89e7f5bf
author: stevestein
ms.author: sstein
ms.openlocfilehash: 38522539230fd35aca058f9a26b53a3f4baa682b
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85889179"
---
# <a name="ihsyscolumns-transact-sql"></a>IHsyscolumns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **IHsyscolumns** view 會公開從非 SQL Server 發行者發佈之發行項的資料行資訊。 這個視圖會儲存在散發資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|資料行或程序參數的名稱。|  
|**id**|**int**|這個資料行所屬資料表的物件識別碼，或這個參數相關聯預存程序的識別碼。|  
|**xtype**|**tinyint**|[sys.sys類型 &#40;transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md)的實體儲存體類型。|  
|**typestat**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xusertype**|**tinyint**|擴充使用者自訂資料類型的識別碼。|  
|**length**|**bigint**|從[sys.sys類型 &#40;transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md)的最大實體儲存體長度。|  
|**xprec**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xscale**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colid**|**int**|資料行或參數識別碼。|  
|**xoffset**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**bitpos**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**留**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**colstat**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**cdefault**|**int**|這個資料行之預設值的識別碼。|  
|**domain**|**int**|這個資料行的規則或 CHECK 條件約束的識別碼。|  
|**number**|**int**|程式分組時的副程式號碼（**0**代表非程式專案）。|  
|**colorder**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**autoval**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**offset**|**int**|這個資料行出現在其中的資料列內位移。|  
|**collationid**|**int**|資料行定序的識別碼。 以非字元為基礎的資料行是 NULL。|  
|**語言**|**int**|資料行的語言識別碼。|  
|**status**|**int**|用來描述資料行或參數屬性的點陣圖：<br /><br /> **0x08** = 資料行允許 null 值。<br /><br /> **0x10** = 當加入**Varchar**或**Varbinary**資料行時，ANSI 填補已生效。 會保留**Varchar**的尾端空白，並保留**Varbinary**資料行的尾端零。<br /><br /> **0x40** = 參數是輸出參數。<br /><br /> **0x80** = 資料行是識別欄位。|  
|**type**|**int**|[sys.sys類型 &#40;transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md)的實體儲存體類型。|  
|**usertype**|**tinyint**|來自sys.sys類型的使用者自訂資料類型的識別碼[&#40;transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md)。|  
|**printfmt**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**prec**|**int**|這個資料行的有效位數層級。|  
|**scale**|**int**|這個資料行的小數位數。|  
|**iscomputed]**|**int**|這是一個旗標，指出這個資料行是否為計算資料行：<br /><br /> **0** = 是非計算。<br /><br /> **1** = 計算的。|  
|**isoutparam**|**int**|指出程序參數是否為輸出參數：<br /><br /> **1** = True。<br /><br /> **0** = False。|  
|**isnullable**|**int**|指出資料行是否允許 Null 值：<br /><br /> **1** = True。<br /><br /> **0** = False。|  
|**定序**|**int**|資料行的定序名稱。 以非字元為基礎的資料行是 NULL。|  
|**tdscollation**|**int**|當在表格式資料流 (TDS) 中傳回時，資料行的定序名稱。|  
  
## <a name="see-also"></a>另請參閱  
 [異質資料庫複寫](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [&#40;Transact-sql&#41;的複寫視圖](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
  
