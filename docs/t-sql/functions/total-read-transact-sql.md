---
title: '@@TOTAL_READ (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/17/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@TOTAL_READ_TSQL'
- '@@TOTAL_READ'
dev_langs:
- TSQL
helpviewer_keywords:
- number of disk reads
- disks [SQL Server], number of disk reads
- '@@TOTAL_READ function'
- total read [SQL Server]
- read activity since last started
ms.assetid: b505fbe9-9569-4f3d-80b9-b64b5109ac98
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4d743ba90c6dc8ea93daa97a56aa341e4ba987cb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68098946"
---
# <a name="x40x40totalread-transact-sql"></a>&#x40;&#x40;TOTAL_READ (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在上次啟動之後，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所進行的磁碟讀取 (不是快取讀取) 數目。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
@@TOTAL_READ  
```  
  
## <a name="return-types"></a>傳回類型  
 **integer**  
  
## <a name="remarks"></a>Remarks  
 若要顯示包含多項 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 統計資料的報表，其中包括讀取和寫入活動，請執行 **sp_monitor**。  
  
## <a name="examples"></a>範例  
 下列範例會顯示傳回迄今 (到目前的日期和時間為止) 的磁碟讀取和寫入總數。  
  
```  
SELECT @@TOTAL_READ AS 'Reads', @@TOTAL_WRITE AS 'Writes', GETDATE() AS 'As of';  
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
 [@@TOTAL_WRITE &#40;Transact-SQL&#41;](../../t-sql/functions/total-write-transact-sql.md)  
  
  
