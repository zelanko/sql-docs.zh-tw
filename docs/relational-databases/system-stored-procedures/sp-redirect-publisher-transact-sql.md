---
title: sp_redirect_publisher （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_redirect_publisher_TSQL
- sp_redirect_publisher
helpviewer_keywords:
- sp_redirect_publisher
ms.assetid: af45e2b2-57fb-4bcd-a58b-e61401fb3b26
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6062522ca6c5c3a311ba2f2c796f791c47e874ab
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252112"
---
# <a name="sp_redirect_publisher-transact-sql"></a>sp_redirect_publisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  為現有的發行者/資料庫配對指定重新導向的發行者。 如果發行者資料庫屬於 Always On 可用性群組，則重新導向的發行者就是與可用性群組相關聯的可用性群組接聽程式名稱。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_redirect_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name'   
    [ , [ @redirected_publisher = ] 'new_publisher' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @original_publisher = ] 'original_publisher'` 原先發行資料庫之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 實例的名稱。 *original_publisher*是**sysname**，沒有預設值。  
  
`[ @publisher_db = ] 'publisher_db'` 所發行的資料庫名稱。 *publisher_db*是**sysname**，沒有預設值。  
  
`[ @redirected_publisher = ] 'redirected_publisher'` 與將成為新發行者之可用性群組相關聯的可用性群組接聽程式名稱。 *redirected_publisher*是**sysname**，沒有預設值。 當可用性群組接聽程式設定為非預設的通訊埠時，請連同接聽程式名稱一起指定通訊埠編號，例如 `'Listenername,51433'`  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 無  
  
## <a name="remarks"></a>Remarks  
 **sp_redirect_publisher**可用來將發行者/資料庫配對與可用性群組的接聽程式產生關聯，以允許將複寫發行者重新導向至 Always On 可用性群組的目前主要複本。 在為包含已發行資料庫的可用性群組設定 AG 接聽程式之後，執行**sp_redirect_publisher** 。  
  
 如果原始發行者端的發行集資料庫已從主要複本的可用性群組中移除，請執行**sp_redirect_publisher** ，但不指定 *\@redirected_publisher*參數的值，以移除發行者/資料庫配對的重新導向。 如需有關在時重新導向發行者的詳細資訊，請參閱[維護&#40;AlwaysOn&#41;發行集資料庫 SQL Server](../../database-engine/availability-groups/windows/maintaining-an-always-on-publication-database-sql-server.md)。  
  
## <a name="permissions"></a>Permissions  
 呼叫者必須是**系統管理員（sysadmin** ）固定伺服器角色的成員、散發資料庫的**db_owner**固定資料庫角色，或是與發行者資料庫相關聯之定義發行集的發行集存取清單的成員。  
  
## <a name="see-also"></a>另請參閱  
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_validate_redirected_publisher &#40;transact-sql&#41; ](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)   
 [sp_get_redirected_publisher &#40;transact-sql&#41; ](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [sp_validate_replica_hosts_as_publishers &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
