---
title: sp_schemafilter （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_schemafilter_TSQL
- sp_schemafilter
helpviewer_keywords:
- sp_schemafilter
ms.assetid: 199e869b-2cd2-44ee-b2ee-69edb06a1bc4
author: stevestein
ms.author: sstein
ms.openlocfilehash: 231796d1678a19106eb89f3039cd755e8385082c
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/05/2019
ms.locfileid: "73633011"
---
# <a name="sp_schemafilter-transact-sql"></a>sp_schemafilter (Transact-SQL)
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
`[ @publisher = ] 'publisher'` 是非 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者的名稱。 *publisher*是**sysname**，沒有預設值。  
  
`[ @schema = ] 'schema'` 是架構的名稱。 *架構*是**sysname**，預設值是 Null。  
  
`[ @operation = ] 'operation'` 是要對此架構採取的動作。 *operation*是**Nvarchar （4）** ，它可以是下列值之一。  
  
|Value|說明|  
|-----------|-----------------|  
|**載入**|將指定的結構描述加入不適合發行的結構描述清單中。|  
|**下拉式**|從不適合發行的結構描述清單中，卸除指定的結構描述。|  
|**説明**|傳回不適合發行的結構描述清單。|  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|說明|  
|-----------------|---------------|-----------------|  
|**schemaname**|**sysname**|這是不適合發行的結構描述名稱。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_schemafilter**只應用於異類發行者。  
  
## <a name="permissions"></a>Permissions  
 只有在散發者端的**系統管理員（sysadmin** ）固定伺服器角色的成員，才能夠執行**sp_schemafilter**。  
  
## <a name="see-also"></a>另請參閱  
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
