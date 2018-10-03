---
title: sp_schemafilter (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_schemafilter_TSQL
- sp_schemafilter
helpviewer_keywords:
- sp_schemafilter
ms.assetid: 199e869b-2cd2-44ee-b2ee-69edb06a1bc4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 02e384763a6415f1de27415bf63f3159bddc394e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47756056"
---
# <a name="spschemafilter-transact-sql"></a>sp_schemafilter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  修改和顯示當列出適合發行的 Oracle 資料表時所排除之結構描述的相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_schemafilter [ @publisher = ] 'publisher'   
   [ , [ @schema = ] 'schema' ]   
   [ , [ @operation = ] 'operation' ]   
```  
  
## <a name="arguments"></a>引數  
 [**@publisher** =] **'***發行者***'**  
 名稱的非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。 *發行者*已**sysname**，沒有預設值。  
  
 [**@schema** =] **'***結構描述***'**  
 這是結構描述的名稱。 *結構描述*已**sysname**，預設值是 NULL。  
  
 [**@operation** =] **'***作業***'**  
 這是在此結構描述上所要採取的動作。 *作業*已**nvarchar(4)**，而且可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**add**|將指定的結構描述加入不適合發行的結構描述清單中。|  
|**卸除**|從不適合發行的結構描述清單中，卸除指定的結構描述。|  
|**說明**|傳回不適合發行的結構描述清單。|  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**schemaname**|**sysname**|這是不適合發行的結構描述名稱。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_schemafilter**只應用於異質性發行者。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**散發者端的固定的伺服器角色可以執行**sp_schemafilter**。  
  
## <a name="see-also"></a>另請參閱  
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
