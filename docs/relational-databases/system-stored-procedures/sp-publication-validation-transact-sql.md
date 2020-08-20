---
description: sp_publication_validation (Transact-SQL)
title: sp_publication_validation (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_publication_validation
- sp_publication_validation_TSQL
helpviewer_keywords:
- sp_publication_validation
ms.assetid: 06be2363-00c0-4936-97c1-7347f294a936
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 02409799b4fe597eb784ffe9d94d645c92cddcd0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485830"
---
# <a name="sp_publication_validation-transact-sql"></a>sp_publication_validation (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  針對指定發行集中的每個發行項來初始化發行項驗證要求。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_publication_validation [ @publication = ] 'publication'  
    [ , [ @rowcount_only = ] type_of_check_requested ]  
    [ , [ @full_or_fast = ] full_or_fast ]  
    [ , [ @shutdown_agent = ] shutdown_agent ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 這是發行集的名稱。 *發行* 集是 **sysname**，沒有預設值。  
  
`[ @rowcount_only = ] 'rowcount_only'` 這是指是否只傳回資料表的資料列計數。 *rowcount_only* 是 **Smallint** ，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**0**|執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 相容總和檢查碼。<br /><br /> 注意：水準篩選發行項時，會執行資料列計數作業而不是總和檢查碼運算。|  
|**1** (預設值)|只執行資料列計數檢查。|  
|**2**|執行資料列計數及二進位總和檢查碼。<br /><br /> 注意：對於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 版訂閱者，只會執行資料列計數驗證。|  
  
`[ @full_or_fast = ] 'full_or_fast'` 這是用來計算資料列計數的方法。 *full_or_fast* 是 **Tinyint** ，而且可以是下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**0**|利用 COUNT(*) 執行完整計數。|  
|**1**|從 **sysindexes**快速算算。 計算 [sys.sys索引](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md) 中的資料列比計算實際資料表中的資料列更快。 不過，因為 [sys.sys索引](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md) 會延遲更新，所以資料列計數可能不正確。|  
|**2** (預設值)|先嘗試快速方法來執行條件式快速計數。 如果快速方法有不同結果，便轉換成完整方法。 如果 *expected_rowcount* 為 Null，且使用預存程式來取得值，就一律會使用完整的計數 ( * ) 。|  
  
`[ @shutdown_agent = ] 'shutdown_agent'` 這是指在驗證完成時是否應該立即關閉散發代理程式。 *shutdown_agent* 是 **bit**，預設值是 **0**。 如果是 **0**，複寫代理程式就不會關閉。 如果是 **1**，則複寫代理程式會在最後一篇文章經過驗證後關閉。  
  
`[ @publisher = ] 'publisher'` 指定非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。 *publisher* 是 **sysname**，預設值是 Null。  
  
> [!NOTE]  
>  在發行者端要求驗證時，不應使用「*發行者*」 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_publication_validation** 用於異動複寫中。  
  
 您可以在發行集相關聯的發行項啟用之後隨時呼叫**sp_publication_validation** 。 您可以手動執行這個程序 (一次)，也可以在定期排程驗證資料的作業中執行這個程序。  
  
 如果您的應用程式有立即更新的訂閱者， **sp_publication_validation** 可能會偵測到偽造的錯誤。 **sp_publication_validation** 先在「發行者」端和「訂閱者」端計算資料列計數或總和檢查碼。 由於在發行者端完成資料列計數或總和檢查碼之後，在訂閱者端完成資料列計數或總和檢查碼之前，立即更新觸發程序可能會將訂閱者的更新傳播給發行者，因此，這些值可能會有所不同。 若要確定在驗證發行集時，並不會變更在訂閱者端和發行者端的值，請在驗證期間，停止在發行者端的 Microsoft 分散式交易協調器 (MS DTC) 服務。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色或 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_publication_validation**。  
  
## <a name="see-also"></a>另請參閱  
 [驗證訂閱者端的資料](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [sp_article_validation &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)   
 [sp_table_validation &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-table-validation-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
