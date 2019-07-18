---
title: IHcolumns (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHcolumns_TSQL
- IHcolumns
dev_langs:
- TSQL
helpviewer_keywords:
- IHcolumns system table
ms.assetid: 5bb027e5-5279-487b-9c33-5f402987253c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9985b0587316641955219eb5179ffd6ed07916d3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990394"
---
# <a name="ihcolumns-transact-sql"></a>IHcolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **IHcolumns**系統資料表會包含一個資料列，每個已發行資料行。 此資料表用來定義發行時，如何表示資料行資料類型從非 SQL Server 發行者這基本上是將非 SQL Server 資料庫管理系統 (DBMS) 之間的資料類型對應和 SQL Server。 這份資料表儲存在散發資料庫中。  
  
## <a name="definition"></a>定義  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**column_id**|**int**|識別已發行的資料行。|  
|**publishercolumn_id**|**int**|將已發行的資料行中儲存的資料行中繼資料產生關聯[IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md)系統資料表。|  
|**name**|**sysname**|指定資料行名稱。|  
|**article_id**|**int**|識別欄位所屬的發行項。|  
|**column_ordinal**|**int**|依序識別欄位。|  
|**mapped_type**|**tinyint**|訂閱者之目的地資料行的資料行資料類型。|  
|**mapped_length**|**bigint**|訂閱者的資料行長度。|  
|**mapped_prec**|**int**|訂閱者的資料行有效位數。|  
|**mapped_scale**|**int**|訂閱者的資料行小數位數。|  
|**mapped_nullable**|**bit**|指出訂閱者端的資料行是否接受 NULL 值，其中**1**表示接受 NULL 值。|  
  
## <a name="see-also"></a>另請參閱  
 [異質資料庫複寫](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視&#40;Transact SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_articlecolumn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sysarticlecolumns&#40;系統檢視&#41; &#40;TRANSACT-SQL&#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)   
 [sysarticlecolumns &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
