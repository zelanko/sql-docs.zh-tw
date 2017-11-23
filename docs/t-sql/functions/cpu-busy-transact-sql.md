---
title: "@@CPU_BUSY (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@CPU_BUSY_TSQL'
- '@@CPU_BUSY'
dev_langs: TSQL
helpviewer_keywords:
- CPU [SQL Server]
- status information [SQL Server], CPU
- ticks [SQL Server]
- time [SQL Server], CPU activity
- '@@CPU_BUSY function'
- statistical information [SQL Server], CPU
- CPU [SQL Server], activity
ms.assetid: 81ae0e64-79fa-4a74-9aa5-37045c4cd211
caps.latest.revision: "36"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 337682a73ae351536af64afca77959cbe6297d7f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40cpubusy-transact-sql"></a>&#x40;&#x40;CPU_BUSY (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上次啟動之後所花的工作時間。 結果是以 CPU 時間遞增 (「刻度」) 來計算，且會針對所有 CPU 來累計，因此，它可能會超出實際的經歷時間。 乘以 @@TIMETICKS 將轉換成百萬分之一秒為單位。
  
> [!NOTE]  
>  如果傳回時間 @@CPU_BUSY 或 @@IO_BUSY 超出大約 49 天的累計 CPU 時間，您會收到算術溢位的警告。 在此情況下，值 @@CPU_BUSY ， @@IO_BUSY 和 @@IDLE 變數也不正確。  
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```
@@CPU_BUSY  
```  
  
## <a name="return-types"></a>傳回型別
**integer**
  
## <a name="remarks"></a>備註  
若要顯示報表，包含多項[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]統計資料，包括 CPU 活動，請執行[sp_monitor](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)。
  
## <a name="examples"></a>範例  
下列範例會顯示傳回迄今 (到目前的日期和時間為止) 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CPU 活動。 為了避免在將值轉換成百萬分之一秒時，發生算術溢位，這個範例會將其中一個值轉換成 `float` 資料類型。
  
```sql
SELECT @@CPU_BUSY * CAST(@@TIMETICKS AS float) AS 'CPU microseconds',   
   GETDATE() AS 'As of' ;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
CPU microseconds As of
---------------- -----------------------
18406250         2006-12-05 17:00:50.600
```
  
## <a name="see-also"></a>另請參閱
[sys.dm_os_sys_info &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)  
[@@IDLE &#40;Transact-SQL&#41;](../../t-sql/functions/idle-transact-sql.md)  
[@@IO_BUSY &#40;Transact-SQL&#41;](../../t-sql/functions/io-busy-transact-sql.md)  
[sp_monitor &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)  
[系統統計函數 &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)
  
  
