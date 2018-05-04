---
title: sp_validate_replica_hosts_as_publishers (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_validate_replica_hosts_as_publishers_TSQL
- sp_validate_replica_hosts_as_publishers
helpviewer_keywords:
- sp_validate_replica_hosts_as_publishers
ms.assetid: 45001fc9-2dbd-463c-af1d-aa8982d8c813
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 61be8b7d28a3ef7d879e69b272bcb47fe2a710cd
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="spvalidatereplicahostsaspublishers-transact-sql"></a>sp_validate_replica_hosts_as_publishers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  **sp_validate_replica_hosts_as_publishers**的延伸**sp_validate_redirected_publisher** ，可讓所有的次要複本進行驗證，而不只是目前主要複本。 **sp_validate_replicat_hosts_as_publisher**驗證整個 Alwayson 複寫拓撲。 **sp_validate_replica_hosts_as_publishers**必須直接在散發者上執行，若要避免雙躍點安全性錯誤 (21892) 使用遠端桌面工作階段。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_validate_replica_hosts_as_publishers   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @redirected_publisher = ] 'new_publisher' output  
```  
  
## <a name="arguments"></a>引數  
 [ **@original_publisher** =] **'***original_publisher***'**  
 當初發行資料庫的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體名稱。 *original_publisher*是**sysname**，沒有預設值。  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 要發行的資料庫名稱。 *publisher_db*是**sysname**，沒有預設值。  
  
 [ **@redirected_publisher** =] **'***redirected_publisher***'**  
 重新導向的目標時**sp_redirect_publisher**針對原始發行者/已發行資料庫配對呼叫。 *redirected_publisher*是**sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
 無。  
  
## <a name="remarks"></a>備註  
 如果項目不存在於發行者和發行資料庫， **sp_validate_redirected_publisher**傳回輸出參數為 null *@redirected_publisher*。 否則會在成功和失敗時都傳回相關聯且重新導向的發行者。  
  
 如果驗證成功， **sp_validate_redirected_publisher**傳回成功指示。  
  
 如果驗證失敗，則會引發適當的錯誤。  **sp_validate_redirected_publisher**全力來引發所有問題並不只是第一個遇到的進行。  
  
> [!NOTE]  
>  在驗證不允許讀取存取或需要指定讀取意圖的次要複本主機時，**sp_validate_replica_hosts_as_publishers** 會失敗並發生下列錯誤。  
>   
>  訊息 21899、層級 11、狀態 1、程序 **sp_hadr_verify_subscribers_at_publisher**、行 109  
>   
>  在重新導向的發行者 'MyReplicaHostName' 上用以判斷原始發行者 'MyOriginalPublisher' 的訂閱者是否有 sysserver 項目之查詢失敗，發生錯誤 '976'，錯誤訊息為「錯誤 976，層級 14，狀態 1，訊息: 目標資料庫 'MyPublishedDB' 正參與可用性群組，目前無法供查詢存取。 資料移動已暫停，或者可用性複本無法進行讀取存取。 若要允許唯讀存取可用性群組中的這個資料庫和其他資料庫，請啟用群組中一個或多個次要可用性複本的讀取存取。  如需詳細資訊，請參閱《 **線上叢書》的＜** ALTER AVAILABILITY GROUP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 陳述式＞。  
>   
>  複本主機 'MyReplicaHostName' 發生了一個或多個發行者驗證錯誤。  
  
## <a name="permissions"></a>Permissions  
 呼叫端必須是屬於**sysadmin**固定伺服器角色、 **db_owner**散發資料庫或定義的發行集的發行集存取清單成員的固定的資料庫角色與發行者資料庫相關聯。  
  
## <a name="see-also"></a>另請參閱  
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_get_redirected_publisher &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [sp_redirect_publisher &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [sp_validate_redirected_publisher &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)  
  
  
