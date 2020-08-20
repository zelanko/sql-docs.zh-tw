---
description: sp_replsetoriginator (Transact-SQL)
title: sp_replsetoriginator (Transact-sql) |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0c75f590fc0482319783d1fb94f516d43581dd39
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88493084"
---
# <a name="sp_replsetoriginator-transact-sql"></a>sp_replsetoriginator (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  在雙向異動複寫中，用來叫用回送偵測和處理。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_replsetoriginator [ @server_name= ] 'server_name'   
    , [ @database_name= ] 'database_name'  
```  
  
## <a name="arguments"></a>引數  
`[ @server_name = ] 'server_name'` 這是套用交易的伺服器名稱。 *originating_server* 是 **sysname**，沒有預設值。  
  
`[ @database_name = ] 'database_name'` 這是套用交易的資料庫名稱。 *originating_db* 是 **sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 **sp_replsetoriginator** 是由散發代理程式執行，以記錄複寫所套用的交易來源。 這項資訊用來叫用已設定回送屬性之雙向交易式訂閱的回送偵測。  
  
## <a name="permissions"></a>權限  
 只有在發行者端的 **系統管理員（sysadmin** ）固定伺服器角色的成員、發行集資料庫的 **db_owner** 固定資料庫角色的成員，或是發行集存取清單中的使用者 (PAL) 可以執行 **sp_replsetoriginator**。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
