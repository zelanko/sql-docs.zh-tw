---
title: sp_prepexecrpc (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepexecrpc
- sp_cursor_prepexecrpc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_prepexecrpc
ms.assetid: 35d686f2-ef31-4eaa-baa9-9cef5d6c87c2
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ab11cbca7177408ed94e79967ab55bad9fbc50b1
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43027952"
---
# <a name="spprepexecrpc-transact-sql"></a>sp_prepexecrpc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  準備及執行已使用 RPC 識別碼來指定的參數化預存程序呼叫。 sp_prepexecrpc 的叫用方式 ID = 14 表格式資料流 (TDS) 封包中的。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_prepexecrpc handle OUTPUT, RPCCall  
    [ , bound_param ] [ ,...n]]  
```  
  
## <a name="arguments"></a>引數  
 *控制代碼*  
 這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產生的已備妥控制代碼識別碼。 *處理*是必要的參數與**int**傳回值。  
  
 *RPCCall*  
 使用 ODBC 標準語法定義預存程序呼叫。 *RPCCall*是必要的參數呼叫**ntext**字串輸入值。  
  
 *bound_param*  
 指定選擇性使用其他參數。 *bound_param*呼叫的任何資料類型，來指定使用中的其他參數的輸入值。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
