---
title: sp_showpendingchanges （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_showpendingchanges
- sp_showpendingchanges_TSQL
helpviewer_keywords:
- sp_showpendingchanges
ms.assetid: 8013a792-639d-4550-b262-e65d30f9d291
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2f6d22fb18989022676eb06751d583383a14d783
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85881496"
---
# <a name="sp_showpendingchanges-transact-sql"></a>sp_showpendingchanges (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  傳回結果集，顯示正等候複寫的變更。 這個預存程序執行於發行集資料庫的發行者端，以及訂閱資料庫的訂閱者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
> [!NOTE]  
>  這個程序會提供變更數目的近似值，以及與這些變更相關的資料列。 例如，此程序會從發行者或訂閱者擷取資訊，但不會同時針對兩者進行。 儲存在另一個節點的資訊可能會使要同步處理的變更集比程序預估的變更集小。  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_showpendingchanges [ [ @destination_server = ] 'destination_server' ]  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article']  
    [ , [ @show_rows = ] show_rows]  
```  
  
## <a name="arguments"></a>引數  
`[ @destination_server = ] 'destination_server'`這是套用所複寫之變更的伺服器名稱。 *destination_server*是**sysname**，預設值是 Null。  
  
`[ @publication = ] 'publication'`這是發行集的名稱。 *發行*集是**sysname**，預設值是 Null。 當指定*發行*集時，結果只限于指定的發行集。  
  
`[ @article = ] 'article'`這是發行項的名稱。 發行項是**sysname**，預設*值是 Null* 。 當*指定了發行*項時，結果只限于指定的發行項。  
  
`[ @show_rows = ] 'show_rows'`指定結果集是否包含有關暫止變更的更多特定資訊，預設值為**0**。 如果指定了**1**的值，結果集會包含 is_delete 和 rowguid 資料行。  
  
## <a name="result-set"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|destination_server|**sysname**|正要複寫變更所在的伺服器名稱。|  
|pub_name|**sysname**|發行集的名稱。|  
|destination_db_name|**sysname**|正要複寫變更所在的資料庫名稱。|  
|is_dest_subscriber|**bit**|指出正要將變更複寫到訂閱者。 值為**1**表示正在將變更複寫到訂閱者。 **0**表示正在將變更複寫到發行者。|  
|article_name|**sysname**|引發變更之資料表的發行項名稱。|  
|pending_deletes|**int**|等候複寫的刪除數目。|  
|pending_ins_and_upd|**int**|等候複寫的插入和更新數目。|  
|is_delete|**bit**|表示暫止變更是否為刪除。 值為**1**表示變更為刪除。 需要的值為**1** @show_rows 。|  
|rowguid|**uniqueidentifier**|識別所變更之資料列的 GUID。 需要的值為**1** @show_rows 。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 sp_showpendingchanges 用於合併式複寫中。  
  
 sp_showpendingchanges 用於疑難排解合併式複寫之時。  
  
 sp_showpendingchanges 的結果並不包含層代 0 的資料列。  
  
 當針對發行項所*指定的發行*項不屬於針對發行集所指定的發行集時 *，* 會傳回0的計數做為 pending_deletes 和 pending_ins_and_upd。  
  
## <a name="permissions"></a>權限  
 只有系統管理員 (sysadmin) 固定伺服器角色或 db_owner 固定資料庫角色的成員，才能夠執行 sp_showpendingchanges。  
  
## <a name="see-also"></a>另請參閱  
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
