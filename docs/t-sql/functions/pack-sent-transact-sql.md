---
title: "@@PACK_SENT (TRANSACT-SQL) |Microsoft 文件"
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
- '@@PACK_SENT'
- '@@PACK_SENT_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- number of output packets written
- '@@PACK_SENT function'
- packets [SQL Server], ouput
- networking [SQL Server], output packets
- connections [SQL Server], packets
- output packets written to network [SQL Server]
ms.assetid: 8a322162-24c9-48e9-bfa4-c060e4e11dba
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2c2a073a94d227514c8a418b396e598649346477
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40packsent-transact-sql"></a>&#x40;&#x40;PACK_SENT (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在上次啟動之後，寫入網路中的輸出封包數目。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
@@PACK_SENT  
```  
  
## <a name="return-types"></a>傳回類型  
 **integer**  
  
## <a name="remarks"></a>備註  
 若要顯示報表，包含多項[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]統計資料，包括封包傳送和接收執行**sp_monitor**。  
  
## <a name="examples"></a>範例  
 下列範例會顯示 `@@PACK_SENT` 的用法。  
  
```  
SELECT @@PACK_SENT AS 'Pack Sent';  
```  
  
 範例結果集如下：  
  
```  
Pack Sent  
-----------  
291  
```  
  
## <a name="see-also"></a>請參閱＜  
 [@@PACK_RECEIVED &#40;Transact-SQL&#41;](../../t-sql/functions/pack-received-transact-sql.md)   
 [sp_monitor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [系統統計函數 &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  
