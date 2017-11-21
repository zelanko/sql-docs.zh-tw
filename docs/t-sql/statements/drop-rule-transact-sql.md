---
title: "卸除規則 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 05/11/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_RULE_TSQL
- DROP RULE
dev_langs:
- TSQL
helpviewer_keywords:
- rules [SQL Server], removing
- deleting roles
- DROP RULE statement
- removing roles
- dropping roles
ms.assetid: 8370b730-7fd5-43fe-a7f6-8300b3caa16d
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ba898b1c9f94f4e38102da929709b4a05f889b7e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="drop-rule-transact-sql"></a>DROP RULE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從目前資料庫移除一或多個使用者自訂的規則。  
  
> [!IMPORTANT]  
>  未來版本將移除 DROP RULE [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 請勿在新的開發工作中使用 DROP RULE，並規劃修改目前使用 DROP RULE 的應用程式。 請改用檢查條件約束，您可以使用的 CHECK 關鍵字建立[CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)或[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)。 如需詳細資訊，請參閱 [Unique Constraints and Check Constraints](../../relational-databases/tables/unique-constraints-and-check-constraints.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
DROP RULE [ IF EXISTS ] { [ schema_name . ] rule_name } [ ,...n ] [ ; ]  
```  
  
## <a name="arguments"></a>引數  
 *如果存在*  
 **適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))。  
  
 只有當它已經存在有條件地卸除規則。  
  
 *schema_name*  
 這是規則所屬的結構描述名稱。  
  
 *規則*  
 這是要移除的規則。 規則名稱必須遵守的規則[識別碼](../../relational-databases/databases/database-identifiers.md)。 您可以選擇性地指定規則結構描述名稱。  
  
## <a name="remarks"></a>備註  
 若要卸除規則，且規則目前繫結了資料行或別名資料類型，請先將它解除繫結。 若要解除繫結規則，請使用**sp_unbindrule**。 如果您試圖卸除規則時，規則仍是繫結的，便會出現一則錯誤訊息，且會取消 DROP RULE 陳述式。  
  
 在卸除規則之後，會輸入規則先前管理的資料行中所輸入的新資料，但不會有規則的條件約束。 現有資料完全不會受到影響。  
  
 DROP RULE 陳述式不適用於 CHECK 條件約束。 如需有關卸除檢查條件約束的詳細資訊，請參閱[ALTER TABLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 若要執行 DROP RULE，使用者至少必須有規則所屬結構描述的 ALTER 權限。  
  
## <a name="examples"></a>範例  
 下列範例會解除繫結再卸除名稱為 `VendorID_rule` 的規則。 
  
```  
sp_unbindrule 'Production.ProductVendor.VendorID'  
DROP RULE VendorID_rule  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE RULE &#40;Transact-SQL&#41;](../../t-sql/statements/create-rule-transact-sql.md)   
 [sp_bindrule &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_unbindrule &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-unbindrule-transact-sql.md)   
 [USE &#40;Transact-SQL&#41;](../../t-sql/language-elements/use-transact-sql.md)  


