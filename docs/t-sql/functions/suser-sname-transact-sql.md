---
description: SUSER_SNAME (Transact-SQL)
title: SUSER_SNAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
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
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5d441cba0f070f4d93210000f3b497e88ebf9011
ms.sourcegitcommit: 197a6ffb643f93592edf9e90b04810a18be61133
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2020
ms.locfileid: "91380063"
---
# <a name="suser_sname-transact-sql"></a>SUSER_SNAME (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  傳回與安全性識別碼 (SID) 相關聯的登入名稱。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
SUSER_SNAME ( [ server_user_sid ] )   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *server_user_sid*  
**適用於**：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本
  
 這是選擇性的登入安全性識別碼。 *server_user_sid* 為 **varbinary(85)**。 *server_user_sid* 可以是任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 使用者或群組的安全性識別碼。 如果未指定 *server_user_sid*，就會傳回目前使用者的相關資訊。 如果參數包含 NULL 一詞，就會傳回 NULL。  
  
## <a name="return-types"></a>傳回型別  
 **nvarchar(128)**  
  
## <a name="remarks"></a>備註  
 SUSER_SNAME 可在 ALTER TABLE 或 CREATE TABLE 中，用來做為 DEFAULT 條件約束。 SUSER_SNAME 可用在選取清單、WHERE 子句及任何允許使用運算式的位置中。 SUSER_SNAME 後面一律必須接著括號，即使未指定任何參數，也是如此。  
  
 當呼叫 SUSER_SNAME 時，如果未設定引數，它會傳回目前安全性內容的名稱。 當利用 EXECUTE AS，在已切換內容的批次內，在未設定引數的情況下呼叫 SUSER_SNAME 時，它會傳回模擬內容的名稱。 當從模擬內容呼叫時，ORIGINAL_LOGIN 會傳回原始內容的名稱。  
  
## <a name="sssdsfull-remarks"></a>[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 備註  
 SUSER_NAME 一律會傳回目前安全性內容的登入名稱。  
  
 SUSER_SNAME 陳述式不支援透過 EXECUTE AS 使用模擬的安全性內容來執行。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-suser_sname"></a>A. 使用 SUSER_SNAME  
 下列範例會傳回目前安全性內容的登入名稱。  
  
```sql
SELECT SUSER_SNAME();  
GO  
```  
  
### <a name="b-using-suser_sname-with-a-windows-user-security-id"></a>B. 搭配 Windows 使用者安全性識別碼使用 SUSER_SNAME  
 下列範例會傳回與 Windows 安全性識別碼相關聯的登入名稱。  
  
**適用於**：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本
  
```sql
SELECT SUSER_SNAME(0x010500000000000515000000a065cf7e784b9b5fe77c87705a2e0000);  
GO  
```  
  
### <a name="c-using-suser_sname-as-a-default-constraint"></a>C. 使用 SUSER_SNAME 做為 DEFAULT 條件約束  
 下列範例會利用 `SUSER_SNAME` 來做為 `DEFAULT` 陳述式中的 `CREATE TABLE` 條件約束。  
  
```sql
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
  
### <a name="d-calling-suser_sname-in-combination-with-execute-as"></a>D. 結合 EXECUTE AS 呼叫 SUSER_SNAME  
 當從模擬內容中呼叫 SUSER_SNAME 時，這個範例會顯示 SUSER_SNAME 的行為。  
  
**適用於**：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本
  
```sql
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
  
## <a name="examples-sssdwfull-and-sspdw"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-suser_sname"></a>E. 使用 SUSER_SNAME  
 下列範例會傳回安全性識別碼值為 `0x01` 的登入名稱。  
  
```sql
SELECT SUSER_SNAME(0x01);  
GO  
```  
  
### <a name="f-returning-the-current-login"></a>F. 傳回目前的登入  
 下列範例會傳回目前登入的登入名稱。  
  
```sql
SELECT SUSER_SNAME() AS CurrentLogin;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [SUSER_SID &#40;Transact-SQL&#41;](../../t-sql/functions/suser-sid-transact-sql.md)   
 [主體 &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md)  
  
  

