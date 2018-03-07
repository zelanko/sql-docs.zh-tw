---
title: "@@PACK_RECEIVED (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
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
- '@@PACK_RECEIVED_TSQL'
- '@@PACK_RECEIVED'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@PACK_RECEIVED function'
- number of packets read
- packets [SQL Server], number read
ms.assetid: 5c0b3d36-bfad-4f0b-abb8-e8f6391b32cd
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1dfa728de6b80397de18bf0bc519c00dfad524ae
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40packreceived-transact-sql"></a>&#x40;&#x40;PACK_RECEIVED (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在上次啟動之後，從網路讀取的輸入封包數目。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
@@PACK_RECEIVED  
```  
  
## <a name="return-types"></a>傳回類型  
 **integer**  
  
## <a name="remarks"></a>備註  
 若要顯示報表，包含多項[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]統計資料，包括封包傳送和接收執行**sp_monitor**。  
  
## <a name="examples"></a>範例  
 下列範例會顯示 `@@PACK_RECEIVED` 的用法。  
  
```  
SELECT @@PACK_RECEIVED AS 'Packets Received';   
```  
  
 範例結果集如下：  
  
```  
Packets Received  
----------------  
128  
```  
  
## <a name="see-also"></a>請參閱＜  
 [@@PACK_SENT](../../t-sql/functions/pack-sent-transact-sql.md)   
 [sp_monitor](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [系統統計函數](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  
