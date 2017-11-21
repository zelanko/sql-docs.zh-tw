---
title: "撤銷系統物件權限 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
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
dev_langs:
- TSQL
helpviewer_keywords:
- REVOKE statement, system objects
- permissions [SQL Server], system objects
ms.assetid: 84983238-dd7d-45bd-99bb-52c9d8e96a87
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 17b371e839d27c065628def8a7be56e6bef650a0
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="revoke-system-object-permissions-transact-sql"></a>REVOKE 系統物件權限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  撤銷系統物件 (如預存程序、擴充預存程序、函數及主體中的檢視) 的權限。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
REVOKE { SELECT | EXECUTE } ON [sys.]system_object FROM principal   
```  
  
## <a name="arguments"></a>引數  
 [**sys。**] .  
 **Sys**限定詞只有時，需要在參考目錄檢視和動態管理檢視。  
  
 *system_object*  
 指定要撤銷其權限的物件。  
  
 *主體*  
 指定要撤銷其權限的主體。  
  
## <a name="remarks"></a>備註  
 這個陳述式可用來撤銷下列項目的權限：某些預存程序、擴充預存程序、資料表值函式、純量函數、檢視、目錄檢視、相容性檢視、INFORMATION_SCHEMA 檢視、動態管理檢視及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝的系統資料表。 這些系統物件在 resource 資料庫中的唯一記錄形式存在 (**mssqlsystemresource**)。 資源資料庫是唯讀的。 物件的連結會公開為中的記錄**sys**每個資料庫的結構描述。  
  
 預設名稱解析會對資源資料庫解析不合格的程序名稱。 因此， **sys。** 在指定目錄檢視和動態管理檢視時，才需要辨識符號。  
  
> [!CAUTION]  
>  撤銷系統物件的權限，會導致相依於這些系統物件的應用程式失敗。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 會使用目錄檢視，但如果您變更了目錄檢視的預設權限，就可能無法按照預期的方式運作。  
  
 不支援撤銷觸發程序的權限及拒絕系統物件之資料行的權限。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升級期間會保留系統物件的權限。  
  
 您可以在 [sys.system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md) 目錄檢視中看到系統物件。  
  
## <a name="permissions"></a>Permissions  
 需要 CONTROL SERVER 權限。  
  
## <a name="examples"></a>範例  
 下列範例會從 `EXECUTE` 撤銷 `sp_addlinkedserver` 的 `public` 權限。  
  
```  
REVOKE EXECUTE ON sys.sp_addlinkedserver FROM public;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sys.system_objects &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md)   
 [sys.database_permissions &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [授與系統物件權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/grant-system-object-permissions-transact-sql.md)   
 [拒絕系統物件權限 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/deny-system-object-permissions-transact-sql.md)  
  
  

