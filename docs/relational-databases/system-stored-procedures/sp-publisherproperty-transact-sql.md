---
description: sp_publisherproperty (Transact-SQL)
title: sp_publisherproperty (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_publisherproperty
- sp_publisherproperty_TSQL
helpviewer_keywords:
- sp_publisherproperty
ms.assetid: 0ed1ebc1-a1bd-4aed-9f46-615c5cf07827
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 459e5c7c702f01cbae74843e4ed8b3152d25626f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89534966"
---
# <a name="sp_publisherproperty-transact-sql"></a>sp_publisherproperty (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  顯示或變更非發行者的發行者屬性 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 這個預存程序執行於散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_publisherproperty [ @publisher = ] 'publisher'   
   [ , [ @propertyname = ] 'propertyname' ]   
   [ , [ @propertyvalue = ] 'propertyvalue' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publisher = ] 'publisher'` 這是異類發行者的名稱。 *publisher* 是 **sysname**，沒有預設值。  
  
`[ @propertyname = ] 'propertyname'` 這是要設定之屬性的名稱。 *propertyname* 是 **sysname**，它可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**xactsetbatching**|如果發行者端的交易分組成在交易上一致的各個組 (稱為 Xactsets)，以便進行後續處理。 [ **已啟用** ] 值表示可以建立 Xactsets，這是預設值。 [ **停用** ] 值表示不會建立新的 Xactsets 來處理現有的 Xactsets。|  
|**xactsetjob**|如果啟用建立 Xactsets 的 Xactsets 作業， 「 **已啟用** 」值表示 Xactset 作業會定期執行，以在「發行者」端建立 Xactsets。 [ **停用** ] 值表示 Xactsets 只有在輪詢發行者的變更時，才會由記錄讀取器代理程式建立。|  
|**xactsetjobinterval**|Xactset 作業的執行間隔 (以分鐘為單位)。|  
  
 如果省略 *propertyname* ，則會傳回所有可設定的屬性。  
  
 `[ @propertyvalue = ] 'propertyvalue'`  
 這是屬性設定的新值。 *propertyvalue* 是 **sysname**，預設值是 Null。 如果省略 *propertyvalue* ，則會傳回屬性的目前設定。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**propertyname**|**sysname**|傳回下列可設定的發行集屬性：<br /><br /> **xactsetbatching**<br /><br /> **xactsetjob**<br /><br /> **xactsetjobinterval**|  
|**propertyvalue**|**sysname**|這是屬性 **名稱** 資料行中的目前設定。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_publisherproperty** 用於非發行者的異動複寫中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 當僅指定 *發行者* 時，結果集會包含所有可設定屬性的目前設定。  
  
 當指定 *propertyname* 時，只有已命名的屬性才會出現在結果集中。  
  
 當指定所有參數時，屬性會改變，不會傳回結果集。  
  
 變更執行中工作的 **xactsetjobinterval** 屬性時，您必須重新開機作業，新的間隔才會生效。  
  
## <a name="permissions"></a>權限  
 只有散發者端的 **系統管理員（sysadmin** ）固定伺服器角色的成員，才可以執行 **sp_publisherproperty**。  
  
## <a name="see-also"></a>另請參閱  
 [設定 Oracle 發行者的交易集作業 &#40;複寫 Transact-SQL 程式設計&#41;](../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
