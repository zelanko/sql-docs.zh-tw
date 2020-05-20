---
title: sp_replsetoriginator （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: 5e1f29f06d7a840ed6628ecd4dc193a4f1c54b82
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82817056"
---
# <a name="sp_replsetoriginator-transact-sql"></a>sp_replsetoriginator (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  在雙向異動複寫中，用來叫用回送偵測和處理。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_replsetoriginator [ @server_name= ] 'server_name'   
    , [ @database_name= ] 'database_name'  
```  
  
## <a name="arguments"></a>引數  
`[ @server_name = ] 'server_name'`這是套用交易的伺服器名稱。 *originating_server*是**sysname**，沒有預設值。  
  
`[ @database_name = ] 'database_name'`這是要套用交易的資料庫名稱。 *originating_db*是**sysname**，沒有預設值。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功）或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 散發代理程式會執行**sp_replsetoriginator** ，以記錄複寫所套用的交易來源。 這項資訊用來叫用已設定回送屬性之雙向交易式訂閱的回送偵測。  
  
## <a name="permissions"></a>權限  
 只有在發行者端的**系統管理員（sysadmin** ）固定伺服器角色成員、發行集資料庫之**db_owner**固定資料庫角色的成員，或是發行集存取清單（PAL）中的使用者，才能夠執行**sp_replsetoriginator**。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
