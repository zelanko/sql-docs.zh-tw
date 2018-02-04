---
title: "MSdatatype_mappings (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSdatatype_mappings
- MSdatatype_mappings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdatatype_mappings view
ms.assetid: 13cdabb3-6e07-4e8d-ae80-4235022ccc7f
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f0acbcbf2c70b08b44e0147989fb1f9dcd3e2301
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="msdatatypemappings-transact-sql"></a>MSdatatype_mappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdatatype_mappings**檢視會將 SQL Server 資料類型對應至非 SQL Server 資料庫管理系統 (DBMS) 所用的資料類型。 這份資料表儲存在**msdb**資料庫。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**dbms_name**|**nvarchar(128)**|這是 DBMS 的名稱。 以下是可能的值和其說明。<br /><br /> **MSSQLSERVER**： 目的地是 SQL Server 資料庫。<br />**ORACLE**： 目的地是一個 Oracle 資料庫。<br />**DB2**： 目的地是 IBM DB2 資料庫。<br />**SYBASE**： 目的地是一個 Sybase 資料庫。|  
|**sql_type**|**nvarchar(128)**|是 SQL Server 資料類型。|  
|**dest_type**|**nvarchar(128)**|為非 SQL Server 資料類型的名稱。|  
|**dest_prec**|**bigint**|為非 SQL Server 資料類型的有效位數。|  
|**dest_create_params**|**int**|僅供內部使用。|  
|**dest_nullable**|**bit**|為非 SQL Server 資料類型是否支援 NULL 值。|  
  
## <a name="see-also"></a>另請參閱  
 [異質資料庫複寫](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [指定 「 Oracle 發行者 」 的資料類型對應](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [複寫資料表 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
