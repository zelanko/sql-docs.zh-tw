---
title: sp_validate_replica_hosts_as_publishers （T-sql）
description: 描述可讓所有次要複本進行驗證的 sp_validate_replica_hosts_as_publishers 預存程式。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_validate_replica_hosts_as_publishers_TSQL
- sp_validate_replica_hosts_as_publishers
helpviewer_keywords:
- sp_validate_replica_hosts_as_publishers
ms.assetid: 45001fc9-2dbd-463c-af1d-aa8982d8c813
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9375be2a2af2b7653b3f0f036405533f1571ff3f
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/20/2019
ms.locfileid: "75319995"
---
# <a name="sp_validate_replica_hosts_as_publishers-transact-sql"></a>sp_validate_replica_hosts_as_publishers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  **sp_validate_replica_hosts_as_publishers**是**sp_validate_redirected_publisher**的延伸，可讓所有次要複本進行驗證，而不只是目前的主要複本。 **sp_validate_replicat_hosts_as_publisher**會驗證整個 Always On 複寫拓撲。 **sp_validate_replica_hosts_as_publishers**必須使用遠端桌面會話直接在散發者端執行，以避免雙躍點安全性錯誤（21892）。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [transact-sql 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_validate_replica_hosts_as_publishers   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @redirected_publisher = ] 'new_publisher' output  
```  
  
## <a name="arguments"></a>引數  
`[ @original_publisher = ] 'original_publisher'`原先發行資料庫之[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實例的名稱。 *original_publisher*是**sysname**，沒有預設值。  
  
`[ @publisher_db = ] 'publisher_db'`要發行之資料庫的名稱。 *publisher_db*是**sysname**，沒有預設值。  
  
`[ @redirected_publisher = ] 'redirected_publisher'`針對原始發行者/已發行的資料庫配對呼叫**sp_redirect_publisher**時，重新導向的目標。 *redirected_publisher*是**sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 無。  
  
## <a name="remarks"></a>備註  
 如果發行者和發行資料庫沒有專案存在， **sp_validate_redirected_publisher**會針對輸出參數* \@redirected_publisher*傳回 null。 否則會在成功和失敗時都傳回相關聯且重新導向的發行者。  
  
 如果驗證成功， **sp_validate_redirected_publisher**會傳回成功指示。  
  
 如果驗證失敗，則會引發適當的錯誤。  **sp_validate_redirected_publisher**會盡力引發所有問題，而不只是第一個遇到的問題。  
  
> [!NOTE]  
>  在驗證不允許讀取存取或需要指定讀取意圖的次要複本主機時， **sp_validate_replica_hosts_as_publishers**將會失敗並出現下列錯誤。  
>   
>  訊息 21899、層級 11、狀態 1、程序 **sp_hadr_verify_subscribers_at_publisher**、行 109  
>   
>  在重新導向的發行者 'MyReplicaHostName' 上用以判斷原始發行者 'MyOriginalPublisher' 的訂閱者是否有 sysserver 項目之查詢失敗，發生錯誤 '976'，錯誤訊息為「錯誤 976，層級 14，狀態 1，訊息: 目標資料庫 'MyPublishedDB' 正參與可用性群組，目前無法供查詢存取。 資料移動已暫停，或者可用性複本無法進行讀取存取。 若要允許唯讀存取可用性群組中的這個資料庫和其他資料庫，請啟用群組中一個或多個次要可用性複本的讀取存取。  如需詳細資訊，請參閱《 **線上叢書》的＜** ALTER AVAILABILITY GROUP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 陳述式＞。  
>   
>  複本主機 'MyReplicaHostName' 發生了一個或多個發行者驗證錯誤。  
  
## <a name="permissions"></a>權限  
 呼叫者必須是**系統管理員（sysadmin** ）固定伺服器角色的成員、散發資料庫的**db_owner**固定資料庫角色，或是與發行者資料庫相關聯之定義發行集的發行集存取清單的成員。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的複寫預存程式](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_get_redirected_publisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [sp_redirect_publisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [sp_validate_redirected_publisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)  
  
  
