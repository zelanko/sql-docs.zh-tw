---
description: sp_validname (Transact-SQL)
title: sp_validname (Transact-sql) |Microsoft Docs
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8b448493ada2d6ec5d1073f194053463b463807b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480948"
---
# <a name="sp_validname-transact-sql"></a>sp_validname (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  檢查有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別碼名稱。 所有的非二進位和非零資料（包括可以使用 **Nchar**、 **Nvarchar**或 **Ntext** 資料類型儲存的 Unicode 資料）都會被視為識別碼名稱的有效字元。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_validname [@name =] 'name'   
     [, [@raise_error =] raise_error]  
```  
  
## <a name="arguments"></a>引數  
`[ @name = ] 'name'` 這是要檢查有效性的 [識別碼](../../relational-databases/databases/database-identifiers.md) 名稱。 *名稱* 是 **sysname**，沒有預設值。 *名稱* 不能是 Null，不能是空字串，也不能包含二進位零字元。  
  
`[ @raise_error = ] raise_error` 指定是否要引發錯誤。 *raise_error* 是 **bit**，預設值是1。 這表示錯誤將會出現。 如果是 0，則表示不會出現任何錯誤訊息。  
  
## <a name="return-code-values"></a>傳回碼值  
 0 (成功) 或 1 (失敗)  
  
## <a name="permissions"></a>權限  
 需要 **public** 角色的成員資格。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的資料庫引擎預存程式 ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [NCHAR &#40;Transact-sql&#41;](../../t-sql/functions/nchar-transact-sql.md)   
 [Nchar 和 Nvarchar &#40;Transact-sql&#41;](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)   
 [Ntext、text 和 image &#40;Transact-sql&#41;](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
