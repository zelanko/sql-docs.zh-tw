---
description: sp_markpendingschemachange (Transact-SQL)
title: sp_markpendingschemachange (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_markpendingschemachange
- sp_markpendingschemachange_TSQL
helpviewer_keywords:
- sp_markpendingschemachange
ms.assetid: 01100309-7bef-4154-85bf-f18489577e37
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0b5b207c4d36e820e6635bd9c8a2e99cdb7e4829
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541688"
---
# <a name="sp_markpendingschemachange-transact-sql"></a>sp_markpendingschemachange (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  用來支援合併式發行集，使管理員能夠略過所選的暫止結構描述變更，因而不會複寫它們。 這個預存程序執行於發行集資料庫的發行者端。  
  
> [!CAUTION]  
>  這個預存程序可以防止複寫結構描述變更。 只有在試過其他方法 (如重新初始化)，且效能成本太高時，才應該利用這個預存程序來解決問題。  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_markpendingschemachange [@publication = ] 'publication'  
    [ , [ @schemaversion = ] schemaversion ]  
    [ , [ @status = ] 'status' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 這是發行集的名稱。 *發行* 集是 **sysname**，沒有預設值。  
  
`[ @schemaversion = ] schemaversion` 識別暫止的架構變更。 *schemaversion* 是 **int**，預設值是 **0**。 使用 [sp_enumeratependingschemachanges &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-enumeratependingschemachanges-transact-sql.md) 列出發行集的暫止架構變更。  
  
`[ @status = ] 'status'` 這是指是否將略過暫止的架構變更。 *狀態*是**Nvarchar (10) **預設值為作用中 **。** 如果 [ *狀態* ] 的值已 **略過**，則不會複寫選取的架構變更。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_markpendingschemachange** 搭配合並式複寫使用。  
  
 **sp_markpendingschemachange** 是一種預存程式，適用于合併式複寫的可支援性，而且只有在其他更正動作（例如重新初始化）無法更正狀況或在效能方面太昂貴時，才應該使用此預存程式。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員（sysadmin** ）固定伺服器角色或 **db_owner** 固定資料庫角色的成員，才能夠執行 **sp_markpendingschemachange**。  
  
## <a name="see-also"></a>另請參閱  
 [sysmergeschemachange &#40;Transact-sql&#41;](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)  
  
  
