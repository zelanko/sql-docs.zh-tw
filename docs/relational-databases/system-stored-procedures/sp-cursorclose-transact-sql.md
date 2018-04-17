---
title: sp_cursorclose (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cursor_close_TSQL
- sp_cursor_close
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorclose
ms.assetid: d9b7b44d-cdff-456e-97df-7031a3b9beb6
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1053cf5b483f2bce87c103bd1ad44fee3bae0455
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="spcursorclose-transact-sql"></a>sp_cursorclose (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  關閉和取消配置資料指標，以及釋放相關聯的所有資源。也就是說，它會卸除用於支援 KEYSET 或 STATIC 的暫存資料表**游標**。 sp_cursorclose 的叫用方式是在表格式資料流 (TDS) 封包中指定 ID = 9。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_cursorclose cursor  
```  
  
## <a name="arguments"></a>引數  
 *cursor*  
 是一個資料指標*處理*所產生值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和 sp_cursoropen 程序所傳回。 *資料指標*是必要的參數呼叫**int**輸入值。  
  
> [!NOTE]  
>  輸入值 -1 會套用到目前連接的所有資料指標上。  
  
## <a name="remarks"></a>備註  
 *資料指標*會傳回錯誤訊息，如果已關閉資料指標之後，已執行的程序，或指定無效的控制代碼。  
  
 RPC 狀態指出整體成功或失敗。  
  
 DONE 資料列計數一定是 0。  
  
## <a name="see-also"></a>另請參閱  
 [sp_cursoropen &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
