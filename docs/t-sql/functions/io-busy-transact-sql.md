---
title: '@@IO_BUSY (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- '@@IO_BUSY'
- '@@IO_BUSY_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- ticks [SQL Server]
- I/O [SQL Server], time spent performing operations
- '@@IO_BUSY function'
- output operations [SQL Server]
- input operations [SQL Server]
- time [SQL Server], I/O operations
ms.assetid: 3c26770c-41ae-4e34-8c82-7bef920ffbca
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 1a5e8338ebebb99f5d7738d53432ebb0dd560771
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="x40x40iobusy-transact-sql"></a>&#x40;&#x40;IO_BUSY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上一次啟動之後，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用來執行輸入和輸出作業的時間。 結果是以 CPU 時間遞增 (「刻度」) 來計算，且會針對所有 CPU 來累計，因此，它可能會超出實際的經歷時間。 乘以 @@TIMETICKS 以轉換成微秒。  
  
> [!NOTE]  
>  若 @@CPU_BUSY 或 @@IO_BUSY 的傳回時間超出大約 49 天的累計 CPU 時間，您會收到算術溢位的警告。 在這個情況下，@@CPU_BUSY、@@IO_BUSY 和 @@IDLE 變數的值並不精確。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
@@IO_BUSY  
```  
  
## <a name="return-types"></a>傳回類型  
 **integer**  
  
## <a name="remarks"></a>Remarks  
 若要顯示包含多項 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 統計資料的報表，請執行 sp_monitor。  
  
## <a name="examples"></a>範例  
 下列範例會顯示傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在開始時間和目前時間之間，用來執行輸入/輸出作業的毫秒數。 為了避免在將值轉換成微秒時發生算術溢位，這個範例會將其中一個值轉換成 **float** 資料類型。  
  
```  
SELECT @@IO_BUSY*@@TIMETICKS AS 'IO microseconds',   
   GETDATE() AS 'as of';  
```  
  
 典型的結果集如下：  
  
```  
  
IO microseconds as of                   
--------------- ----------------------  
4552312500      12/5/2006 10:23:00 AM   
```  
  
## <a name="see-also"></a>另請參閱  
 [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [@@CPU_BUSY &#40;Transact-SQL&#41;](../../t-sql/functions/cpu-busy-transact-sql.md)   
 [sp_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [系統統計函式 &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  
