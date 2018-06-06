---
title: REVOKE 系統物件權限 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
ms.openlocfilehash: d5b83f7d0f3a1ed09ab57445d8c769d24a0b1ca9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
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
 [**sys.**] .  
 只有在參考目錄檢視和動態管理檢視時，才需要 **sys** 限定詞。  
  
 *system_object*  
 指定要撤銷其權限的物件。  
  
 *principal*  
 指定要撤銷其權限的主體。  
  
## <a name="remarks"></a>Remarks  
 這個陳述式可用來撤銷下列項目的權限：某些預存程序、擴充預存程序、資料表值函式、純量函數、檢視、目錄檢視、相容性檢視、INFORMATION_SCHEMA 檢視、動態管理檢視及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝的系統資料表。 在資源資料庫 (**mssqlsystemresource**) 中，每一個系統物件都會以唯一記錄的形式存在。 資源資料庫是唯讀的。 該物件的連結會公開為每個資料庫 **sys** 結構描述中的記錄。  
  
 預設名稱解析會對資源資料庫解析不合格的程序名稱。 因此，只有在指定目錄檢視和動態管理檢視時，才需要 **sys.** 限定詞。  
  
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
 [sys.system_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [GRANT 系統物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-system-object-permissions-transact-sql.md)   
 [DENY 系統物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/deny-system-object-permissions-transact-sql.md)  
  
  
