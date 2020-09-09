---
description: sp_monitor (Transact-SQL)
title: sp_monitor (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_monitor_TSQL
- sp_monitor
dev_langs:
- TSQL
helpviewer_keywords:
- sp_monitor
ms.assetid: cb628496-2f9b-40e4-b018-d0831c4cb018
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f214abb7b20c42ec62f1bc35d85222e0033798d1
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544744"
---
# <a name="sp_monitor-transact-sql"></a>sp_monitor (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  顯示相關的統計資料 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_monitor  
```  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="result-sets"></a>結果集  
  
|欄名|描述|  
|-----------------|-----------------|  
|**last_run**|上次執行的時間 **sp_monitor** 。|  
|**current_run**|正在執行 **sp_monitor** 時間。|  
|**seconds**|自執行 **sp_monitor** 以來經過的秒數。|  
|**cpu_busy**|伺服器電腦的 CPU 已執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 工作的秒數。|  
|**io_busy**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已花在處理輸入和輸出作業的秒數。|  
|**閒置**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已閒置的秒數。|  
|**packets_received**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已讀取的輸入封包數。|  
|**packets_sent**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已寫入的輸出封包數。|  
|**packet_errors**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在讀取和寫入封包時所發現的錯誤數。|  
|**total_read**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的讀取數。|  
|**total_write**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的寫入數。|  
|**total_errors**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在讀取和寫入時所發現的錯誤數。|  
|**連接**|登入或嘗試登入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的次數。|  
  
## <a name="remarks"></a>備註  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會透過一系列的函數來持續追蹤它已完成的工作量。 執行 **sp_monitor** 會顯示這些函式所傳回的目前值，並顯示自上一次執行程式之後的變更量。  
  
 針對每個資料行，統計資料會以表單 *號碼* (*數位*) -*數位*% 或 *數位* (*號碼*) 列印。 第一個 *數位* 指的是 (**cpu_busy**、 **io_busy**和 **閒置**) 的秒數，或在重新開機後 (其他變數的總數目) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 括弧中的 *數位* 指的是上一次執行 **sp_monitor** 後的秒數或總數。 百分比是自上次執行 **sp_monitor** 以來的時間百分比。 例如，如果報表顯示 **cpu_busy** 為 4250 (215) -68%，表示自上次啟動以來，cpu 已忙碌4250秒、上次 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行 **sp_monitor** 以來的215秒數，以及自上次執行 **sp_monitor** 以來的總時間的68%。  
  
## <a name="permissions"></a>權限  
 需要 **系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會報告有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 忙碌情形的資訊。  
  
```console
USE master  
EXEC sp_monitor  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

```console
last_run       current_run                   seconds
-----------    --------------------------    ---------
Mar 29 1998    11:55AM Apr 4 1998 2:22 PM    561

cpu_busy           io_busy     idle
---------------    ---------   --------------
190(0)-0%          187(0)-0%   148(556)-99%

packets_received       packets_sent    packet_errors
----------------       ------------    -------------
16(1)                  20(2)           0(0)

total_read     total_write   total_errors    connections
-----------    -----------   -------------   -----------
141(0)         54920(127)    0(0)            4(0)
```
  
## <a name="see-also"></a>另請參閱  
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
