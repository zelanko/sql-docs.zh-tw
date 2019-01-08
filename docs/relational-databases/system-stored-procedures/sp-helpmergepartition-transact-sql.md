---
title: sp_helpmergepartition & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergepartition
- sp_helpmergepartition_TSQL
helpviewer_keywords:
- sp_helpmergepartition
ms.assetid: 184188cc-f519-445d-97ce-aae38f1eb550
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 673baf1b41e3ffcceaa635191352af376008313e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52779350"
---
# <a name="sphelpmergepartition-transact-sql"></a>sp_helpmergepartition (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回指定合併式發行集的資料分割資訊。 這個預存程序執行於任何資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpmergepartition [ @publication= ] 'publication'   
    [ , [ @suser_sname = ] 'suser_sname' ]  
    [ , [ @host_name = ] 'host_name' ]  
```  
  
## <a name="arguments"></a>引數  
 [  **@publication=** ] **'***發行集***'**  
 這是發行集的名稱。 *發行集*已**sysname**，沒有預設值。  
  
 [  **@suser_sname=** ] **'***suser_sname***'**  
 這是用來定義資料分割的 SUSER_SNAME 值。 *suser_sname*已**sysname**，預設值是 NULL。 請提供這個參數，將結果集限制於 SUSER_SNAME 解析成所提供的值之資料分割。  
  
> [!NOTE]  
>  當*suser_sname*提供，則*host_name*必須是 NULL  
  
 [  **@host_name=** ] **'***host_name***'**  
 這是用來定義資料分割的 HOST_NAME 值。 *host_name*已**sysname**，預設值是 NULL。 請提供這個參數，將結果集限制於 HOST_NAME 解析成所提供的值之資料分割。  
  
> [!NOTE]  
>  當*suser_sname*提供，則*host_name*必須是 NULL  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**資料分割**|**int**|識別訂閱者資料分割。|  
|**host_name**|**sysname**|值，用於建立訂用帳戶的資料分割篩選的值時[HOST_NAME](../../t-sql/functions/host-name-transact-sql.md)函式，在訂閱者。|  
|**suser_sname**|**sysname**|值，用於建立訂用帳戶的資料分割篩選的值時[SUSER_SNAME](../../t-sql/functions/suser-sname-transact-sql.md)函式，在訂閱者。|  
|**dynamic_snapshot_location**|**nvarchar(255)**|訂閱者的資料分割之篩選資料快照集的位置。|  
|**date_refreshed**|**datetime**|上次執行快照集作業來產生資料分割的篩選資料快照集的日期。|  
|**dynamic_snapshot_jobid**|**uniqueidentifier**|識別建立資料分割之篩選資料快照集的作業。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_helpmergepartition**用於合併式複寫中。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色並**db_owner**固定的資料庫角色可以執行**sp_helpmergepartition**。  
  
## <a name="see-also"></a>另請參閱  
 [sp_addmergepartition &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md)   
 [sp_dropmergepartition &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepartition-transact-sql.md)  
  
  
