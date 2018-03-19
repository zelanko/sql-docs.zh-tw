---
title: "DENY 系統物件權限 (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
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
- DENY statement, system objects
- encryption [SQL Server], system objects
- system objects [SQL Server]
- cryptography [SQL Server], system objects
ms.assetid: 4e43f954-0982-470b-a239-08a13c61563a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8d584aa3c7329b8f81e445f612e7041cd14e0747
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="deny-system-object-permissions-transact-sql"></a>DENY 系統物件權限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  拒絕系統物件 (如預存程序、擴充預存程序、函數及檢視) 的權限。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
DENY { SELECT | EXECUTE } ON [ sys.]system_object TO principal   
```  
  
## <a name="arguments"></a>引數  
 [ **sys.**]  
 只有在參考目錄檢視和動態管理檢視時，才需要 **sys** 限定詞。  
  
 *system_object*  
 指定要拒絕其權限的物件。  
  
 *principal*  
 指定要撤銷其權限的主體。  
  
## <a name="remarks"></a>Remarks  
 這個陳述式可用來拒絕下列項目的權限：某些預存程序、擴充預存程序、資料表值函式、純量函數、檢視、目錄檢視、相容性檢視、INFORMATION_SCHEMA 檢視、動態管理檢視及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝的系統資料表。 在資源資料庫 (**mssqlsystemresource**) 中，這些系統物件會個別以唯一記錄形式存在。 資源資料庫是唯讀的。 該物件的連結會公開為每個資料庫 **sys** 結構描述中的記錄。  
  
 預設名稱解析會對資源資料庫解析不合格的程序名稱。 因此，只有在指定目錄檢視和動態管理檢視時，才需要 **sys** 限定詞。  
  
> [!CAUTION]  
>  拒絕系統物件的權限，會導致相依於這些系統物件的應用程式失敗。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 會使用目錄檢視，但如果您變更了目錄檢視的預設權限，就可能無法按照預期的方式運作。  
  
 不支援拒絕觸發程序的權限及拒絕系統物件之資料行的權限。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升級期間會保留系統物件的權限。  
  
 您可以在 [sys.system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md) 目錄檢視中看到系統物件。 您可以在 [master](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) 資料庫的 **sys.database_permissions** 目錄檢視中，看到系統物件的權限。  
  
 下列查詢會傳回系統物件權限的相關資訊：  
  
```  
SELECT * FROM master.sys.database_permissions AS dp   
    JOIN sys.system_objects AS so  
    ON dp.major_id = so.object_id  
    WHERE dp.class = 1 AND so.parent_object_id = 0 ;  
GO  
```  
  
## <a name="permissions"></a>Permissions  
 需要 CONTROL SERVER 權限。  
  
## <a name="examples"></a>範例  
 下列範例會對 `EXECUTE` 拒絕 `xp_cmdshell` 的 `public` 權限。  
  
```  
DENY EXECUTE ON sys.xp_cmdshell TO public;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [Transact-SQL 語法慣例 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [GRANT 系統物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-system-object-permissions-transact-sql.md)   
 [REVOKE 系統物件權限 &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-system-object-permissions-transact-sql.md)  
  
  
