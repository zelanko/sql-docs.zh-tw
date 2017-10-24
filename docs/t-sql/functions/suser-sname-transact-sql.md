---
title: "SUSER_SNAME (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SUSER_SNAME_TSQL
- SUSER_SNAME
dev_langs:
- TSQL
helpviewer_keywords:
- security identification names [SQL Server]
- logins [SQL Server], users
- SIDs [SQL Server]
- SUSER_SNAME function
- users [SQL Server], logins
- logins [SQL Server], names
- IDs [SQL Server], logins
- identification numbers [SQL Server], logins
- names [SQL Server], logins
ms.assetid: 11ec7d86-d429-4004-a436-da25df9f8761
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 35e3429d49940cd863cd04fc336226268ddf61c9
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="susersname-transact-sql"></a>SUSER_SNAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回與安全性識別碼 (SID) 相關聯的登入名稱。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
SUSER_SNAME ( [ server_user_sid ] )   
```  
  
## <a name="arguments"></a>引數  
 *server_user_sid*  
**適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 這是選擇性的登入安全性識別碼。 *server_user_sid*是**varbinary(85)**。 *server_user_sid*可以是任何的安全性識別碼[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登入或[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows 使用者或群組。 如果*server_user_sid*是未指定，會傳回目前使用者相關資訊。 如果參數包含 NULL 一詞，就會傳回 NULL。  
  
## <a name="return-types"></a>傳回類型  
 **nvarchar （128)**  
  
## <a name="remarks"></a>備註  
 SUSER_SNAME 可在 ALTER TABLE 或 CREATE TABLE 中，用來做為 DEFAULT 條件約束。 SUSER_SNAME 可用在選取清單、WHERE 子句及任何允許使用運算式的位置中。 SUSER_SNAME 後面一律必須接著括號，即使未指定任何參數，也是如此。  
  
 當呼叫 SUSER_SNAME 時，如果未設定引數，它會傳回目前安全性內容的名稱。 當利用 EXECUTE AS，在已切換內容的批次內，在未設定引數的情況下呼叫 SUSER_SNAME 時，它會傳回模擬內容的名稱。 當從模擬內容呼叫時，ORIGINAL_LOGIN 會傳回原始內容的名稱。  
  
## <a name="includesssdsfullincludessssdsfull-mdmd-remarks"></a>[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]備註  
 SUSER_NAME 一律會傳回目前安全性內容的登入名稱。  
  
 SUSER_SNAME 陳述式不支援透過 EXECUTE AS 使用模擬的安全性內容來執行。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-susersname"></a>A. 使用 SUSER_SNAME  
 下列範例會傳回目前安全性內容的登入名稱。  
  
```  
SELECT SUSER_SNAME();  
GO  
```  
  
### <a name="b-using-susersname-with-a-windows-user-security-id"></a>B. 搭配 Windows 使用者安全性識別碼使用 SUSER_SNAME  
 下列範例會傳回與 Windows 安全性識別碼相關聯的登入名稱。  
  
**適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT SUSER_SNAME(0x010500000000000515000000a065cf7e784b9b5fe77c87705a2e0000);  
GO  
```  
  
### <a name="c-using-susersname-as-a-default-constraint"></a>C. 使用 SUSER_SNAME 做為 DEFAULT 條件約束  
 下列範例會利用 `SUSER_SNAME` 來做為 `DEFAULT` 陳述式中的 `CREATE TABLE` 條件約束。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE sname_example  
(  
login_sname sysname DEFAULT SUSER_SNAME(),  
employee_id uniqueidentifier DEFAULT NEWID(),  
login_date  datetime DEFAULT GETDATE()  
);   
GO  
INSERT sname_example DEFAULT VALUES;  
GO  
```  
  
### <a name="d-calling-susersname-in-combination-with-execute-as"></a>D. 結合 EXECUTE AS 呼叫 SUSER_SNAME  
 當從模擬內容中呼叫 SUSER_SNAME 時，這個範例會顯示 SUSER_SNAME 的行為。  
  
**適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT SUSER_SNAME();  
GO  
EXECUTE AS LOGIN = 'WanidaBenShoof';  
SELECT SUSER_SNAME();  
REVERT;  
GO  
SELECT SUSER_SNAME();  
GO  
  
```  
  
 以下是結果。  
  
 ```
sa  
WanidaBenShoof  
sa
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-susersname"></a>E. 使用 SUSER_SNAME  
 下列範例會傳回安全性識別碼值為 `0x01` 的登入名稱。  
  
```  
SELECT SUSER_SNAME(0x01);  
GO  
```  
  
### <a name="f-returning-the-current-login"></a>F. 傳回目前的登入  
 下列範例會傳回目前的登入的登入名稱。  
  
```  
SELECT SUSER_SNAME() AS CurrentLogin;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [SUSER_SID &#40;TRANSACT-SQL &#41;](../../t-sql/functions/suser-sid-transact-sql.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [執行 AS &#40;TRANSACT-SQL &#41;](../../t-sql/statements/execute-as-transact-sql.md)  
  
  


