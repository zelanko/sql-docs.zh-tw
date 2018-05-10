---
title: GRANT 系統物件權限 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
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
- encryption [SQL Server], system objects
- system objects [SQL Server]
- GRANT statement, system objects
ms.assetid: 9d4e89f4-478f-419a-8b50-b096771e3880
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 39130687751acab7c86051625f41db644b567a8c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="grant-system-object-permissions-transact-sql"></a>GRANT 系統物件權限 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  授與系統物件 (如系統預存程序、擴充預存程序、函數及檢視) 的權限。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
GRANT { SELECT | EXECUTE } ON [ sys.]system_object TO principal   
```  
  
## <a name="arguments"></a>引數  
 [ sys.] .  
 只有在參考目錄檢視和動態管理檢視時，才需要 sys 限定詞。  
  
 *system_object*  
 指定要授與其權限的物件。  
  
 *principal*  
 指定要對其授與權限的主體。  
  
## <a name="remarks"></a>Remarks  
 這個陳述式可用來授與下列項目的權限：某些預存程序、擴充預存程序、資料表值函式、純量函數、檢視、目錄檢視、相容性檢視、INFORMATION_SCHEMA 檢視、動態管理檢視及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝的系統資料表。 在伺服器的資源資料庫 (mssqlsystemresource) 中，這些系統物件會個別以唯一記錄形式存在。 資源資料庫是唯讀的。 該物件的連結會公開為每個資料庫之 sys 結構描述中的記錄。 可以授與、拒絕及撤銷執行或選取系統物件的權限。  
  
 授與執行或選取某物件的權限，不一定會轉讓所有使用該物件所需的權限。 大部分的物件所執行的作業都需要其他權限。 例如，被授與 sp_addlinkedserver 之 EXECUTE 權限的使用者無法建立連結伺服器，除非該使用者也是系統管理員 (sysadmin) 固定伺服器角色的成員。  
  
 預設名稱解析會對資源資料庫解析不合格的程序名稱。 因此，只有在指定目錄檢視和動態管理檢視時，才需要 sys 限定詞。  
  
 不支援授與觸發程序的權限及授與系統物件之資料行的權限。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升級期間會保留系統物件的權限。  
  
 您可以在 [sys.system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md) 目錄檢視中看到系統物件。 您可以在 master 資料庫的 [sys.database_permissions](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) 目錄檢視中，看到系統物件的權限。  
  
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
  
### <a name="a-granting-select-permission-on-a-view"></a>A. 授與檢視的 SELECT 權限  
 下列範例授與選取檢視 (這份檢視會列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入) 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入 `Sylvester1` 權限。 接著，這個範例再授與其他權限，它是檢視非使用者擁有之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入上的中繼資料時所需的權限。  
  
```  
USE AdventureWorks2012;  
GRANT SELECT ON sys.sql_logins TO Sylvester1;  
GRANT VIEW SERVER STATE to Sylvester1;  
GO  
```  
  
### <a name="b-granting-execute-permission-on-an-extended-stored-procedure"></a>B. 授與擴充預存程序的 EXECUTE 權限  
 下列範例會對 `EXECUTE` 授與 `xp_readmail` 的 `Sylvester1` 權限。  
  
```  
GRANT EXECUTE ON xp_readmail TO Sylvester1;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [sys.system_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [REVOKE System Object Permissions &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-system-object-permissions-transact-sql.md)   
 [DENY System Object Permissions &#40;Transact-SQL&#41;](../../t-sql/statements/deny-system-object-permissions-transact-sql.md)  
  
  
