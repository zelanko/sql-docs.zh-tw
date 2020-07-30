---
title: Replication Views （Transact-sql） |Microsoft Docs
description: 複寫視圖包含 SQL Server 中複寫所使用的資訊。 這些檢視可以方便您存取複寫系統資料表中的資料。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: ab4088aa563befcb32eaaf8fe129716b789f516b
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243609"
---
# <a name="replication-views-transact-sql"></a>複寫檢視表 (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  這些 views 包含中複寫所使用的資訊 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 這些視圖可讓您更輕鬆地存取複寫[系統資料表](../../relational-databases/system-tables/replication-tables-transact-sql.md)中的資料。 檢視是在使用者資料庫被當作發行集或訂閱資料庫啟用時，在該資料庫中建立。 當使用者資料庫從複寫拓撲中移除時，所有的複寫物件都會從使用者資料庫中一併移除。 存取複寫中繼資料的慣用方法是使用複寫[預存程式](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)。  
  
> [!IMPORTANT]  
>  系統檢視不應該直接被任何使用者變更。  
  
## <a name="replication-views"></a>複寫檢視  
 下列是複寫所用的系統檢視清單，這些系統檢視是根據資料庫加以分組。  
  
### <a name="replication-views-in-the-msdb-database"></a>msdb 資料庫中的複寫資料庫  

:::row:::
    :::column:::
        [MSdatatype_mappings &#40;Transact-sql&#41;](../../relational-databases/system-views/msdatatype-mappings-transact-sql.md)
    :::column-end:::
    :::column:::
        [msdb.dbo.sysdatatypemappings 以 &#40;Transact-sql&#41;](../../relational-databases/system-views/sysdatatypemappings-transact-sql.md)
    :::column-end:::
:::row-end:::

### <a name="replication-views-in-the-distribution-database"></a>散發資料庫中的複寫檢視  

:::row:::
    :::column:::
        [IHextendedArticleView &#40;Transact-sql&#41;](../../relational-databases/system-views/ihextendedarticleview-transact-sql.md)

        [IHextendedSubscriptionView &#40;Transact-sql&#41;](../../relational-databases/system-views/ihextendedsubscriptionview-transact-sql.md)

        [IHsyscolumns &#40;Transact-sql&#41;](../../relational-databases/system-views/ihsyscolumns-transact-sql.md)

        [MSdistribution_status &#40;Transact-sql&#41;](../../relational-databases/system-views/msdistribution-status-transact-sql.md)

        [sysarticlecolumns &#40;System View&#41; &#40;Transact-sql&#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)
    :::column-end:::
    :::column:::
        [sysarticles &#40;System View&#41; &#40;Transact-sql&#41;](../../relational-databases/system-views/sysarticles-system-view-transact-sql.md)

        [sysextendedarticlesview &#40;Transact-sql&#41;](../../relational-databases/system-views/sysextendedarticlesview-transact-sql.md)

        [syspublications &#40;系統檢視&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/syspublications-system-view-transact-sql.md)

        [syssubscriptions &#40;系統檢視&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/syssubscriptions-system-view-transact-sql.md)
    :::column-end:::
:::row-end:::

### <a name="replication-views-in-the-publication-database"></a>發行集資料庫中的複寫檢視  

:::row:::
    :::column:::
        [sysmergeextendedarticlesview &#40;Transact-sql&#41;](../../relational-databases/system-views/sysmergeextendedarticlesview-transact-sql.md)

        [systranschemas &#40;Transact-sql&#41;](../../relational-databases/system-views/systranschemas-transact-sql.md)
    :::column-end:::
    :::column:::
        [sysmergepartitioninfoview &#40;Transact-sql&#41;](../../relational-databases/system-views/sysmergepartitioninfoview-transact-sql.md)
    :::column-end:::
:::row-end:::

### <a name="replication-views-in-the-subscription-database"></a>訂閱資料庫中的複寫檢視  

:::row:::
    :::column:::
        [sysmergeextendedarticlesview &#40;Transact-sql&#41;](../../relational-databases/system-views/sysmergeextendedarticlesview-transact-sql.md)

        [sysmergepartitioninfoview &#40;Transact-sql&#41;](../../relational-databases/system-views/sysmergepartitioninfoview-transact-sql.md)
    :::column-end:::
    :::column:::
        [systranschemas &#40;Transact-sql&#41;](../../relational-databases/system-views/systranschemas-transact-sql.md)
    :::column-end:::
:::row-end:::
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
