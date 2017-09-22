---
title: "@@IO_BUSY (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 48e1bcd5a80825715ad6aed8649dad843e92c1ea
ms.contentlocale: zh-tw
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40iobusy-transact-sql"></a>（& s) #x 40; & #x 40; IO_BUSY (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上一次啟動之後，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用來執行輸入和輸出作業的時間。 結果是以 CPU 時間遞增 (「刻度」) 來計算，且會針對所有 CPU 來累計，因此，它可能會超出實際的經歷時間。 乘以@TIMETICKS將轉換成百萬分之一秒為單位。  
  
> [!NOTE]  
>  如果傳回時間@CPU_BUSY，@@IO_BUSY超出大約 49 天的累計 CPU 時間，您會收到算術溢位的警告。 在此情況下，值 @@CPU_BUSY，@@IO_BUSY和 @@IDLE變數也不正確。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
@@IO_BUSY  
```  
  
## <a name="return-types"></a>傳回類型  
 **integer**  
  
## <a name="remarks"></a>備註  
 若要顯示包含多項 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 統計資料的報表，請執行 sp_monitor。  
  
## <a name="examples"></a>範例  
 下列範例會顯示傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在開始時間和目前時間之間，用來執行輸入/輸出作業的毫秒數。 若要將值轉換成微秒時，請避免算術溢位，範例會將轉換其中一個值來**float**資料型別。  
  
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
 [sys.dm_os_sys_info &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [@@CPU_BUSY &#40;Transact-SQL&#41;](../../t-sql/functions/cpu-busy-transact-sql.md)   
 [sp_monitor &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [系統統計函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  

