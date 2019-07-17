---
title: sp_replsetoriginator (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replsetoriginator
- sp_replsetoriginator_TSQL
helpviewer_keywords:
- sp_replsetoriginator
ms.assetid: 030e5226-0585-439f-b8cd-36f48367d86d
author: stevestein
ms.author: sstein
ms.openlocfilehash: dd3e27e935d7774c3882e8cc46430542351dd87c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68113156"
---
# <a name="spreplsetoriginator-transact-sql"></a>sp_replsetoriginator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在雙向異動複寫中，用來叫用回送偵測和處理。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_replsetoriginator [ @server_name= ] 'server_name'   
    , [ @database_name= ] 'database_name'  
```  
  
## <a name="arguments"></a>引數  
`[ @server_name = ] 'server_name'` 是套用交易的伺服器名稱。 *originating_server*已**sysname**，沒有預設值。  
  
`[ @database_name = ] 'database_name'` 套用交易的情況下是資料庫的名稱。 *originating_server*已**sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_replsetoriginator**執行散發代理程式記錄的複寫所套用的交易來源。 這項資訊用來叫用已設定回送屬性之雙向交易式訂閱的回送偵測。  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色，在 「 發行者 」 的成員**db_owner**固定的資料庫角色，發行集資料庫，或在發行集存取清單 (PAL) 中的使用者可以執行**sp_replsetoriginator**。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
