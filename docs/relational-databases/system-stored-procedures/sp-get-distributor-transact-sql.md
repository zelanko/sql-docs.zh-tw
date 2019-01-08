---
title: sp_get_distributor & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_get_distributor
- sp_get_distributor_TSQL
helpviewer_keywords:
- sp_get_distributor
ms.assetid: f0134448-bc17-4f2f-bd81-619351ce56ac
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ccdc8529bb62e4e1db15f0a5ea85a64c5b679abf
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52760180"
---
# <a name="spgetdistributor-transact-sql"></a>sp_get_distributor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  判斷散發者是否安裝在伺服器中。 這個預存程序執行於任何資料庫中散發者所在的電腦。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_get_distributor   
```  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**安裝**|**int**|**0** = 否;**1** = yes|  
|**發佈伺服器**|**sysname**|散發者伺服器的名稱|  
|**安裝的散發資料庫**|**int**|**0** = 否;**1** = yes|  
|**散發發行者**|**int**|**0** = 否;**1** = yes|  
|**具有遠端散發發行者**|**int**|**0** = 否;**1** = yes|  
  
## <a name="remarks"></a>備註  
 **sp_get_distributor**主要是供[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]快照、 交易式和合併式複寫中。  
  
## <a name="permissions"></a>Permissions  
 任何使用者都可以執行**sp_get_distributor**。 非 NULL 結果集時，會傳回此預存程序執行的成員**db_owner**或是**replmonitor**固定資料庫角色的成員的散發資料庫上**db_owner**固定的資料庫角色的至少一個已發行的資料庫。 非 NULL 結果集也會傳回此預存程序由使用者執行發行集存取清單 (PAL) 中的至少一個已發行資料庫，還是也可以執行在散發資料庫的非 SQL Server 發行者的 PAL ﹜**預存程序_get_distributor**。  
  
## <a name="see-also"></a>另請參閱  
 [設定發行和散發](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [散發者與發行者資訊指令碼](../../relational-databases/replication/administration/distributor-and-publisher-information-script.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
