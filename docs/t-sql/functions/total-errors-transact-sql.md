---
title: "@@TOTAL_ERRORS (TRANSACT-SQL) |Microsoft 文件"
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
- '@@TOTAL_ERRORS'
- '@@TOTAL_ERRORS_TSQL'
dev_langs: TSQL
helpviewer_keywords:
- '@@TOTAL_ERRORS function'
- total errors [SQL Server]
- errors [SQL Server], read/write
- number of disk read/write errors
- disks [SQL Server], errors
- write errors [SQL Server]
- read/write errors
ms.assetid: 09e62428-ee0e-4ef5-b969-da9d255f1199
caps.latest.revision: "18"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 53065810884eaae4513f5f8a2725f136daaaa5e4
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40totalerrors-transact-sql"></a>&#x40;&#x40;TOTAL_ERRORS (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在上次啟動之後，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所發生的磁碟寫入錯誤數目。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
@@TOTAL_ERRORS  
```  
  
## <a name="return-types"></a>傳回類型  
 **integer**  
  
## <a name="remarks"></a>備註  
 這個函數並不會將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所發現的所有寫入錯誤都計算在內。 伺服器本身會處理不常發生的非嚴重寫入錯誤，這些錯誤不會被視為錯誤。 若要顯示報表，包含多項[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行統計資料，包括錯誤的總數**sp_monitor**。  
  
## <a name="examples"></a>範例  
 這個範例會顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 迄今 (到目前的日期和時間為止) 所發現的錯誤數目。  
  
```  
SELECT @@TOTAL_ERRORS AS 'Errors', GETDATE() AS 'As of';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Errors      As of                   
----------- ----------------------  
0           3/28/2003 12:32:11 PM   
```  
  
## <a name="see-also"></a>請參閱＜  
 [sp_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [系統統計函數 &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  
