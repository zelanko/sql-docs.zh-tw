---
title: "xp_sprintf (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- xp_sprintf_TSQL
- xp_sprintf
dev_langs: TSQL
helpviewer_keywords: xp_sprintf
ms.assetid: 1eedd65c-03cc-4eab-b76e-04684fdfec52
caps.latest.revision: "33"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7619be5f36b1086609d4950ad0dad365d60a5a95
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="xpsprintf-transact-sql"></a>xp_sprintf (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  將字串輸出參數中的一系列字元和值加以格式化並且儲存。 每一個格式引數都會取代成對應的引數。  
  
||  
|-|  
|**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。|  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
xp_sprintf { string OUTPUT , format }  
     [ , argument [ ,...n ] ]  
```  
  
## <a name="arguments"></a>引數  
 *string*  
 是**varchar**接收輸出的變數。  
  
 OUTPUT  
 當指定這個引數時，它會將變數值放在輸出參數中。  
  
 *格式*  
 格式字元字串，其中含有預留位置*引數*值，類似於 C 語言支援的**sprintf**函式。 目前只支援 %s 格式引數。  
  
 *引數*  
 這是代表對應格式引數值的字元字串。  
  
 *n*  
 這是表示最多可以指定 50 個引數的預留位置。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 **xp_sprintf**傳回下列訊息：  
  
 `The command(s) completed successfully.`  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色的成員資格。  
  
## <a name="see-also"></a>請參閱＜  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [一般擴充預存程序 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_sscanf &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/xp-sscanf-transact-sql.md)  
  
  
