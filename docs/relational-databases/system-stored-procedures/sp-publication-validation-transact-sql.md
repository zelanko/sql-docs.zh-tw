---
title: sp_publication_validation （Transact-sql） |Microsoft Docs
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: bdfe70e3df86f792d250cd7abcc3ef3013e9df19
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056227"
---
# <a name="sp_publication_validation-transact-sql"></a>sp_publication_validation (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

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
`[ @publication = ] 'publication'` 是發行集的名稱。 *發行*集是**sysname**，沒有預設值。  
  
`[ @rowcount_only = ] 'rowcount_only'` 是指是否只傳回資料表的資料列計數。 *rowcount_only*是**Smallint** ，而且可以是下列其中一個值。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**0**|執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 相容總和檢查碼。<br /><br /> 注意：當水準篩選發行項時，會執行資料列計數作業，而不是總和檢查碼作業。|  
|**1** (預設值)|只執行資料列計數檢查。|  
|**2**|執行資料列計數及二進位總和檢查碼。<br /><br /> 注意：對於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本7.0 訂閱者，只會執行資料列計數驗證。|  
  
`[ @full_or_fast = ] 'full_or_fast'` 是用來計算資料列計數的方法。 *full_or_fast*是**Tinyint** ，而且可以是下列其中一個值。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**0**|利用 COUNT(*) 執行完整計數。|  
|**1**|會從**sysindexes**快速計數。 計算[sysindexes](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md)中的資料列，比計算實際資料表中的資料列快很多。 不過，因為[sysindexes](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md)會延遲更新，所以資料列計數可能不正確。|  
|**2** (預設值)|先嘗試快速方法來執行條件式快速計數。 如果快速方法有不同結果，便轉換成完整方法。 如果*expected_rowcount*是 Null，而預存程式是用來取得值，則一律會使用完整的 COUNT （*）。|  
  
`[ @shutdown_agent = ] 'shutdown_agent'` 是在驗證完成時，散發代理程式是否應立即關閉。 *shutdown_agent*是**bit**，預設值是**0**。 如果是**0**，就不會關閉複寫代理程式。 如果是**1**，則複寫代理程式會在驗證最後一篇文章之後關閉。  
  
`[ @publisher = ] 'publisher'` 指定非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的發行者。 *publisher*是**sysname**，預設值是 Null。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者上要求驗證時，不應使用*publisher* 。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>Remarks  
 **sp_publication_validation**用於異動複寫中。  
  
 啟用發行集相關聯的發行項之後，隨時都可以呼叫**sp_publication_validation** 。 您可以手動執行這個程序 (一次)，也可以在定期排程驗證資料的作業中執行這個程序。  
  
 如果您的應用程式有立即更新的訂閱者， **sp_publication_validation**可能會偵測到虛假錯誤。 **sp_publication_validation**會先在「發行者」端，然後在「訂閱者」端計算資料列計數或總和檢查碼。 由於在發行者端完成資料列計數或總和檢查碼之後，在訂閱者端完成資料列計數或總和檢查碼之前，立即更新觸發程序可能會將訂閱者的更新傳播給發行者，因此，這些值可能會有所不同。 若要確定在驗證發行集時，並不會變更在訂閱者端和發行者端的值，請在驗證期間，停止在發行者端的 Microsoft 分散式交易協調器 (MS DTC) 服務。  
  
## <a name="permissions"></a>Permissions  
 只有**系統管理員（sysadmin** ）固定伺服器角色或**db_owner**固定資料庫角色的成員，才能夠執行**sp_publication_validation**。  
  
## <a name="see-also"></a>另請參閱  
 [驗證訂閱者端的資料](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [sp_article_validation &#40;transact-sql&#41; ](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)   
 [sp_table_validation &#40;transact-sql&#41; ](../../relational-databases/system-stored-procedures/sp-table-validation-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
