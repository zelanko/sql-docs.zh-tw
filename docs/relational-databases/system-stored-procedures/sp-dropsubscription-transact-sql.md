---
title: sp_dropsubscription （Transact-sql） |Microsoft Docs
description: 卸載發行者上發行項、發行集或訂閱的訂閱。 這個預存程式會在發行集資料庫的發行者端執行。
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropsubscription
- sp_dropsubscription_TSQL
helpviewer_keywords:
- sp_dropsubscription
ms.assetid: 7551f345-5510-4684-ab53-f9057249d13a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3ef0707d0e2f2770a241ad22be567fed16ad9e3b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85783033"
---
# <a name="sp_dropsubscription-transact-sql"></a>sp_dropsubscription (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  卸除對於發行者的特定發行項、發行集或訂閱集的訂閱。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_dropsubscription [ [ @publication= ] 'publication' ]  
    [ , [ @article= ] 'article' ]  
        , [ @subscriber= ] 'subscriber'  
    [ , [ @destination_db= ] 'destination_db' ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
    [ , [ @reserved= ] 'reserved' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'`這是相關聯發行集的名稱。 *發行*集是**sysname**，預設值是 Null。 如果是**all**，就會取消指定之訂閱者之所有發行集的所有訂閱。 *發行*集是必要參數。  
  
`[ @article = ] 'article'`這是發行項的名稱。 發行項是**sysname**，預設*值是 Null* 。 如果是**all**，就會卸載每個指定發行集和訂閱者之所有發行項的訂閱。 對於允許立即更新的發行集，請使用 [**全部**]。  
  
`[ @subscriber = ] 'subscriber'`這是將卸載其訂閱的訂閱者名稱。 *訂閱者*是**sysname**，沒有預設值。 如果是**all**，就會卸載所有訂閱者的所有訂閱。  
  
`[ @destination_db = ] 'destination_db'`這是目的地資料庫的名稱。 *destination_db*是**sysname**，預設值是 Null。 如果是 NULL，就會卸除這個訂閱者的所有訂閱。  
  
`[ @ignore_distributor = ] ignore_distributor`  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @reserved = ] 'reserved'`  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_dropsubscription**用於快照式和異動複寫中。  
  
 如果您在立即同步發行集中卸除發行項的訂閱，則除非您卸除發行集所有發行項的訂閱，再同時將它們全部重新加入，否則便無法重新加入它們。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_droptransubscription](../../relational-databases/replication/codesnippet/tsql/sp-dropsubscription-tran_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有**系統管理員（sysadmin** ）固定伺服器角色、 **db_owner**固定資料庫角色或建立訂閱之使用者的成員，才能夠執行**sp_dropsubscription**。  
  
## <a name="see-also"></a>另請參閱  
 [刪除發送訂閱](../../relational-databases/replication/delete-a-push-subscription.md)   
 [sp_addsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_changesubstatus &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changesubstatus-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
