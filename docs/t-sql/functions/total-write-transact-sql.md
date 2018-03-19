---
title: '@@TOTAL_WRITE (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@TOTAL_WRITE'
- '@@TOTAL_WRITE_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- write activity since last started [SQL Server]
- number of disk writes
- '@@TOTAL_WRITE function'
- disks [SQL Server], numbr of disk writes
- total write [SQL Server]
ms.assetid: cd528126-51ee-4aa4-a21f-f32ce5c80fac
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e24b92f6eb47e0aa8087e9526e299f2e1e251f0f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40totalwrite-transact-sql"></a>&#x40;&#x40;TOTAL_WRITE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在上次啟動之後，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所進行的磁碟寫入數目。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
@@TOTAL_WRITE  
```  
  
## <a name="return-types"></a>傳回類型  
 **integer**  
  
## <a name="remarks"></a>Remarks  
 若要顯示包含多項 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 統計資料的報表，其中包括讀取和寫入活動，請執行 **sp_monitor**。  
  
## <a name="examples"></a>範例  
 下列範例會顯示傳回迄今 (到目前的日期和時間為止) 的磁碟讀取和寫入總數。  
  
```  
SELECT @@TOTAL_READ AS 'Reads', @@TOTAL_WRITE AS 'Writes', GETDATE() AS 'As of'  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Reads       Writes      As of                   
----------- ----------- ----------------------  
7760        97263       12/5/2006 10:23:00 PM   
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [系統統計函式 &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)   
 [@@TOTAL_READ &#40;Transact-SQL&#41;](../../t-sql/functions/total-read-transact-sql.md)  
  
  
