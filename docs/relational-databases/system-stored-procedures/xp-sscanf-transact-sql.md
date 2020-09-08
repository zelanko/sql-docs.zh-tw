---
description: xp_sscanf (Transact-SQL)
title: xp_sscanf (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_sscanf_TSQL
- xp_sscanf
dev_langs:
- TSQL
helpviewer_keywords:
- xp_sscanf
ms.assetid: 619a9df1-7008-407e-a75a-bc6f851454a8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 53bf62fe03371b4406d5538f8ffe441e2f8970d6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2020
ms.locfileid: "89525324"
---
# <a name="xp_sscanf-transact-sql"></a>xp_sscanf (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  將資料從字串讀入每一個格式引數指定的引數位置中。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
xp_sscanf { string OUTPUT , format } [ ,argument [ ,...n ] ]   
```  
  
## <a name="arguments"></a>引數  
 **string**  
 這是要從中讀取引數值的字元字串。  
  
 OUTPUT  
 指定時，會將 *引數* 值放在 output 參數中。  
  
 *format*  
 是格式化的字元字串，類似于 C 語言 **sscanf** 函式所支援的字串。 目前只支援 %s 格式引數。  
  
 *引數*  
 這是將 **Varchar** 變數設定為對應的 *格式* 引數的值。  
  
 *n*  
 這是表示最多可以指定 50 個引數的預留位置。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="result-sets"></a>結果集  
 **xp_sscanf** 會傳回下列訊息：  
  
 `Command(s) completed successfully.`  
  
## <a name="permissions"></a>權限  
 需要 **public** 角色的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例會利用 `xp_sscanf`，根據值在來源字串格式中的位置，從來源字串擷取兩個值。  
  
```  
DECLARE @filename varchar (20), @message varchar (20);  
EXEC xp_sscanf 'sync -b -fproducts10.tmp -rrandom', 'sync -b -f%s -r%s',   
  @filename OUTPUT, @message OUTPUT;  
SELECT @filename, @message;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-------------------- --------------------   
products10.tmp        random  
```  
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [&#40;Transact-sql&#41;的一般擴充預存程式 ](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_sprintf &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/xp-sprintf-transact-sql.md)  
  
  
