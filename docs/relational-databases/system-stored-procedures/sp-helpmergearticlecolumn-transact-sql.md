---
description: sp_helpmergearticlecolumn (Transact-SQL)
title: sp_helpmergearticlecolumn (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergearticlecolumn
- sp_helpmergearticlecolumn_TSQL
helpviewer_keywords:
- sp_helpmergearticlecolumn
ms.assetid: 651c017b-9e9a-48f2-a0bd-6fc896eab334
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f85830c11ca64f3540995411a2cfe1dac6044544
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474026"
---
# <a name="sp_helpmergearticlecolumn-transact-sql"></a>sp_helpmergearticlecolumn (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  傳回合併式發行集之指定資料表或檢視發行項中的資料行清單。 由於預存程序沒有資料行，因此，如果將這個預存程序指定為發行項，它會傳回錯誤。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helpmergearticlecolumn [ @publication = ] 'publication' ]  
        , [ @article= ] 'article' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 這是發行集的名稱。*發行* 集是 **sysname**，沒有預設值。  
  
`[ @article = ] 'article'` 這是要取得資訊的發行項所在的資料表或視圖名稱。*文章* 是 **sysname**，沒有預設值。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**column_id**|**sysname**|識別欄位。|  
|**column_name**|**sysname**|這是資料表或檢視的資料行名稱。|  
|**發表**|**bit**|指定是否已發行資料行名稱。<br /><br /> **1** 指定正在發行資料行。<br /><br /> **0** 指定未發行。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_helpmergearticlecolumn** 用於合併式複寫中。  
  
## <a name="permissions"></a>權限  
 只有散發資料庫中的 **replmonitor** 固定資料庫角色成員，或是發行集的發行集存取清單中，才可以執行 **sp_helpmergearticlecolumn**。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
