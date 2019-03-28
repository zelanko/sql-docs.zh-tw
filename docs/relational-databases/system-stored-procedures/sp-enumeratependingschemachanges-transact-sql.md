---
title: sp_enumeratependingschemachanges & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_enumeratependingschemachanges
- sp_enumeratependingschemachanges_TSQL
helpviewer_keywords:
- sp_enumeratependingschemachanges
ms.assetid: df169b21-d10a-41df-b3a1-654cfb58bc21
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8a3f0fa918d0247f5fd6dbe11c4a91a2376c52dd
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58530810"
---
# <a name="spenumeratependingschemachanges-transact-sql"></a>sp_enumeratependingschemachanges (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回所有暫止結構描述變更的清單。 這個預存程序可以搭配[sp_markpendingschemachange](../../relational-databases/system-stored-procedures/sp-markpendingschemachange-transact-sql.md)，讓管理員略過所選的暫止的結構描述變更，使它們不會複寫。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_enumeratependingschemachanges [ @publication = ] 'publication'   
    [ , [ @starting_schemaversion = ] starting_schemaversion ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 是發行集名稱。 *發行集*已**sysname**，沒有預設值。  
  
`[ @starting_schemaversion = ] starting_schemaversion` 是的最低數字的結構描述變更来包含在結果集。  
  
## <a name="result-set"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**article_name**|**sysname**|結構描述變更套用的發行項名稱或**發行集全**套用至整個發行集的結構描述變更。|  
|**schemaversion**|**int**|暫止結構描述變更的編號。|  
|**schematype**|**sysname**|代表結構描述變更類型的文字值。|  
|**schematext**|**nvarchar(max)**|描述結構描述變更的 [!INCLUDE[tsql](../../includes/tsql-md.md)]。|  
|**schemastatus**|**nvarchar(10)**|指出發行項的結構描述變更是否暫止，它可以是下列值之一：<br /><br /> **active** = 結構描述變更已暫止<br /><br /> **非使用中**= 結構描述變更為非使用中<br /><br /> **略過**= 不複寫結構描述變更|  
|**schemaguid**|**uniqueidentifier**|識別結構描述變更。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_enumeratependingschemachanges**用於合併式複寫中。  
  
 **sp_enumeratependingschemachanges**，搭配[sp_markpendingschemachange](../../relational-databases/system-stored-procedures/sp-markpendingschemachange-transact-sql.md)，適用於合併式複寫的支援能力，且應該使用只有當其他修正動作，例如重新初始化，無法更正這種情況。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_enumeratependingschemachanges**。  
  
## <a name="see-also"></a>另請參閱  
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sysmergeschemachange &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)  
  
  
