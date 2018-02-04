---
title: "複寫檢視 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
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
dev_langs:
- TSQL
helpviewer_keywords:
- distribution databases [SQL Server replication], system views
- metadata [SQL Server], views
- views [SQL Server], replication
- replication views [SQL Server]
- publications [SQL Server replication], system views
- articles [SQL Server replication], system views
- replication metadata [SQL Server]
- subscriptions [SQL Server replication], system views
- system views [SQL Server], replication
ms.assetid: 93e5056d-0d93-4a48-ba33-72762eb995d8
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 98cf79d757e639a1187becbb9cfaa63c0fe7ff4f
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="replication-views-transact-sql"></a>複寫檢視表 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  這些檢視包含資訊，以供複寫的[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 檢視可讓資料更容易存取[複寫系統資料表](../../relational-databases/system-tables/replication-tables-transact-sql.md)。 檢視是在使用者資料庫被當作發行集或訂閱資料庫啟用時，在該資料庫中建立。 當使用者資料庫從複寫拓撲中移除時，所有的複寫物件都會從使用者資料庫中一併移除。 存取複寫中繼資料的慣用的方法是使用[複寫預存程序](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)。  
  
> [!IMPORTANT]  
>  系統檢視不應該直接被任何使用者變更。  
  
## <a name="replication-views"></a>複寫檢視  
 下列是複寫所用的系統檢視清單，這些系統檢視是根據資料庫加以分組。  
  
### <a name="replication-views-in-the-msdb-database"></a>msdb 資料庫中的複寫資料庫  
  
|||  
|-|-|  
|[MSdatatype_mappings &#40;TRANSACT-SQL &#41;](../../relational-databases/system-views/msdatatype-mappings-transact-sql.md)|[sysdatatypemappings &#40;TRANSACT-SQL &#41;](../../relational-databases/system-views/sysdatatypemappings-transact-sql.md)|  
  
### <a name="replication-views-in-the-distribution-database"></a>散發資料庫中的複寫檢視  
  
|||  
|-|-|  
|[IHextendedArticleView &#40;TRANSACT-SQL &#41;](../../relational-databases/system-views/ihextendedarticleview-transact-sql.md)|[sysarticles &#40;系統檢視 &#41;&#40;TRANSACT-SQL &#41;](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)|  
|[IHextendedSubscriptionView &#40;TRANSACT-SQL &#41;](../../relational-databases/system-views/ihextendedsubscriptionview-transact-sql.md)|[sysextendedarticlesview &#40;TRANSACT-SQL &#41;](../../relational-databases/system-views/sysextendedarticlesview-transact-sql.md)|  
|[IHsyscolumns &#40;Transact-SQL&#41;](../../relational-databases/system-views/ihsyscolumns-transact-sql.md)|[syspublications &#40;系統檢視&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/syspublications-system-view-transact-sql.md)|  
|[MSdistribution_status &#40;TRANSACT-SQL &#41;](../../relational-databases/system-views/msdistribution-status-transact-sql.md)|[syssubscriptions &#40;系統檢視&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/syssubscriptions-system-view-transact-sql.md)|  
|[sysarticlecolumns &#40;系統檢視 &#41;&#40;TRANSACT-SQL &#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)||  
  
### <a name="replication-views-in-the-publication-database"></a>發行集資料庫中的複寫檢視  
  
|||  
|-|-|  
|[sysmergeextendedarticlesview &#40;TRANSACT-SQL &#41;](../../relational-databases/system-views/sysmergeextendedarticlesview-transact-sql.md)|[sysmergepartitioninfoview &#40;TRANSACT-SQL &#41;](../../relational-databases/system-views/sysmergepartitioninfoview-transact-sql.md)|  
|[systranschemas &#40;Transact-SQL&#41;](../../relational-databases/system-views/systranschemas-transact-sql.md)||  
  
### <a name="replication-views-in-the-subscription-database"></a>訂閱資料庫中的複寫檢視  
  
|||  
|-|-|  
|[sysmergeextendedarticlesview &#40;TRANSACT-SQL &#41;](../../relational-databases/system-views/sysmergeextendedarticlesview-transact-sql.md)|[sysmergepartitioninfoview &#40;TRANSACT-SQL &#41;](../../relational-databases/system-views/sysmergepartitioninfoview-transact-sql.md)|  
|[systranschemas &#40;Transact-SQL&#41;](../../relational-databases/system-views/systranschemas-transact-sql.md)||  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
