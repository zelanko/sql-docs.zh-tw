---
title: xp_sprintf （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 01/09/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_sprintf_TSQL
- xp_sprintf
dev_langs:
- TSQL
helpviewer_keywords:
- xp_sprintf
ms.assetid: 1eedd65c-03cc-4eab-b76e-04684fdfec52
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3ba1648da108762b03155eb93e1ee11c53a75583
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "75831769"
---
# <a name="xp_sprintf-transact-sql"></a>xp_sprintf (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  將字串輸出參數中的一系列字元和值加以格式化並且儲存。 每一個格式引數都會取代成對應的引數。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
xp_sprintf { string OUTPUT , format }  
     [ , argument [ ,...n ] ]  
```  
  
## <a name="arguments"></a>引數  
 *字串*  
 這是接收輸出的**Varchar**變數。  
  
 OUTPUT  
 當指定這個引數時，它會將變數值放在輸出參數中。  
  
 *編排*  
 這是具有*引數*值之預留位置的格式字元字串，類似于 C 語言**sprintf**函數所支援的。 目前只支援 %s 格式引數。  
  
 *引數*  
 這是代表對應格式引數值的字元字串。  
  
 *n*  
 這是表示最多可以指定 50 個引數的預留位置。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 **xp_sprintf**會傳回下列訊息：  
  
 `The command(s) completed successfully.`  
  
## <a name="permissions"></a>權限  
 需要 **public** 角色的成員資格。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [&#40;Transact-sql 的一般擴充預存程式&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_sscanf &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/xp-sscanf-transact-sql.md)  
  
  
