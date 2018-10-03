---
title: sp_validname (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_validname
- sp_validname_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_validname
ms.assetid: d51c53c2-1332-407f-b725-4983f2e710eb
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 68e3cd191dc397574e739faa62f315f018bcb466
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47836666"
---
# <a name="spvalidname-transact-sql"></a>sp_validname (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  檢查有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別碼名稱。 所有非二進位和非零值資料，包括可以使用儲存的 Unicode 資料**nchar**， **nvarchar**，或**ntext**資料型別，會被視為有效字元識別項名稱。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_validname [@name =] 'name'   
     [, [@raise_error =] raise_error]  
```  
  
## <a name="arguments"></a>引數  
 [ **@name=** ] **'***name***'**  
 是的名稱[識別碼](../../relational-databases/databases/database-identifiers.md)用來檢查有效性。 *名稱*已**sysname**，沒有預設值。 *名稱*不能是 NULL、 不可為空字串，並不能包含二進位零字元。  
  
 [  **@raise_error=** ] *raise_error&lt*  
 指定是否要引發錯誤。 *raise_error&lt*已**元**，預設值是 1。 這表示錯誤將會出現。 如果是 0，則表示不會出現任何錯誤訊息。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色的成員資格。  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [NCHAR &#40;Transact-SQL&#41;](../../t-sql/functions/nchar-transact-sql.md)   
 [nchar 和 nvarchar &#40;-SQL&AMP;#41;&#41;](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)   
 [ntext、 text 和 image &#40;-SQL&AMP;#41;&#41;](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
