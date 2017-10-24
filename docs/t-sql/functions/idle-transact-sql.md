---
title: "@@IDLE (TRANSACT-SQL) |Microsoft 文件"
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
- '@@IDLE_TSQL'
- '@@IDLE'
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], idle
- ticks [SQL Server]
- '@@IDLE function'
- status information [SQL Server], idle time
- idle time [SQL Server]
ms.assetid: 8f49c62a-8da5-4afd-a5eb-4df8ef8be755
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: ab308bcb1fd3ffdda8e901b2238111abaddecb81
ms.contentlocale: zh-tw
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40idle-transact-sql"></a>&#x40;&#x40; 閒置 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上次啟動之後所經歷的閒置時間。 結果是以 CPU 時間遞增 (「刻度」) 來計算，且會針對所有 CPU 來累計，因此，它可能會超出實際的經歷時間。 乘以@TIMETICKS將轉換成百萬分之一秒為單位。  
  
> [!NOTE]  
>  如果傳回時間@CPU_BUSY，@@IO_BUSY超出大約 49 天的累計 CPU 時間，您會收到算術溢位的警告。 在此情況下，值 @@CPU_BUSY，@@IO_BUSY和 @@IDLE變數也不正確。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
@@IDLE  
```  
  
## <a name="return-types"></a>傳回類型  
 **integer**  
  
## <a name="remarks"></a>備註  
 若要顯示報表，包含多項[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]統計資料，執行**sp_monitor**。  
  
## <a name="examples"></a>範例  
 下列範例會顯示傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在開始時間和目前時間之間所經歷的閒置毫秒數。 為了避免在將值轉換成百萬分之一秒時，發生算術溢位，這個範例會將其中一個值轉換成 `float` 資料類型。  
  
```  
SELECT @@IDLE * CAST(@@TIMETICKS AS float) AS 'Idle microseconds',  
   GETDATE() AS 'as of';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
I  
Idle microseconds  as of                   
----------------- ----------------------  
8199934           12/5/2006 10:23:00 AM   
```  
  
## <a name="see-also"></a>另請參閱  
 [@@CPU_BUSY &#40;Transact-SQL&#41;](../../t-sql/functions/cpu-busy-transact-sql.md)   
 [sp_monitor &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [@@IO_BUSY &#40;Transact-SQL&#41;](../../t-sql/functions/io-busy-transact-sql.md)   
 [系統統計函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  

