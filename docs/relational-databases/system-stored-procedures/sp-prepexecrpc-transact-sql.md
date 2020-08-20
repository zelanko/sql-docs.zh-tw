---
description: sp_prepexecrpc (Transact-SQL)
title: sp_prepexecrpc (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepexecrpc
- sp_cursor_prepexecrpc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_prepexecrpc
ms.assetid: 35d686f2-ef31-4eaa-baa9-9cef5d6c87c2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5f97a95b2976f24a12035efb492f49553f2aa5c1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473856"
---
# <a name="sp_prepexecrpc-transact-sql"></a>sp_prepexecrpc (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  準備及執行已使用 RPC 識別碼來指定的參數化預存程序呼叫。 sp_prepexecrpc 是以 (TDS) 封包的表格式資料流程中的識別碼 = 14 來叫用。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_prepexecrpc handle OUTPUT, RPCCall  
    [ , bound_param ] [ ,...n]]  
```  
  
## <a name="arguments"></a>引數  
 *處理*  
 這是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產生的已備妥控制代碼識別碼。 *控制碼* 是具有 **int** 傳回值的必要參數。  
  
 *RPCCall*  
 使用 ODBC 標準語法定義預存程序呼叫。 *RPCCall* 是一個必要參數，會呼叫 **Ntext** 字串輸入值。  
  
 *bound_param*  
 指定選擇性使用其他參數。 *bound_param* 會呼叫任何資料類型的輸入值，以指定使用中的其他參數。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
