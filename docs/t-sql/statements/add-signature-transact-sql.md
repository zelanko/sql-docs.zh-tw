---
description: ADD SIGNATURE (Transact-SQL)
title: ADD SIGNATURE (Transact-SQL)
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ADD SIGNATURE
- ADD_SIGNATURE_TSQL
helpviewer_keywords:
- ADD SIGNATURE statement
- adding digital signatures
- signatures [SQL Server]
- digital signatures [SQL Server]
ms.assetid: 64d8b682-6ec1-4e5b-8aee-3ba11e72d21f
author: VanMSFT
ms.author: vanto
ms.reviewer: ''
ms.custom: ''
ms.date: 06/10/2020
ms.openlocfilehash: da1072eb299fa4ad65e82210126a9a6f8af25619
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488107"
---
# <a name="add-signature-transact-sql"></a>ADD SIGNATURE (Transact-SQL)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

將數位簽章加入至預存程序、函數、組件或觸發程序。 也將副署簽章加入至預存程序、函數、組件或觸發程序。

![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

## <a name="syntax"></a>語法

```syntaxsql
ADD [ COUNTER ] SIGNATURE TO module_class::module_name
    BY <crypto_list> [ ,...n ]
  
<crypto_list> ::=  
    CERTIFICATE cert_name  
    | CERTIFICATE cert_name [ WITH PASSWORD = 'password' ]
    | CERTIFICATE cert_name WITH SIGNATURE = signed_blob
    | ASYMMETRIC KEY Asym_Key_Name  
    | ASYMMETRIC KEY Asym_Key_Name [ WITH PASSWORD = 'password'.]
    | ASYMMETRIC KEY Asym_Key_Name WITH SIGNATURE = signed_blob
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數

*module_class*  
這是要加入簽章之模組的類別。 結構描述範圍模組的預設值是 OBJECT。  
  
 *module_name*  
 這是要簽署或反簽署的預存程序、函數、組件或觸發程序的名稱。  
  
 CERTIFICATE *cert_name*  
 這是用來預存程序、函數、組件或觸發程序要簽署或反簽署的憑證名稱。  
  
 WITH PASSWORD ='*password*'  
 這是要將憑證私密金鑰或非對稱金鑰解密所需的密碼。 唯有當私密金鑰不受資料庫主要金鑰保護時，才需要這個子句。  
  
 SIGNATURE =*signed_blob*  
 指定模組已簽署的二進位大型物件 (BLOB)。 如果您想要傳送模組但不傳送私密金鑰，則這個子句很有用。 當您使用這個子句時，只需要模組、簽章和公開金鑰，即可將簽署的二進位大型物件加入資料庫中。 *signed_blob* 是十六進位格式的 Blob 本身。  
  
 ASYMMETRIC KEY *Asym_Key_Name*  
 這是預存程序、函數、組件或觸發程序用來簽署或副署的非對稱金鑰名稱。  
  
## <a name="remarks"></a>備註

簽署或副署的模組及用來簽署的憑證或非對稱金鑰必須已存在。 模組中的每個字元都會包含在簽章計算中。 這包括開頭的歸位字元和換行字元。  
  
 可用任何數目的憑證和非對稱金鑰來簽署和副署模組。  
  
 當模組變更時，會卸除模組的簽章。  
  
 如果模組包含 EXECUTE AS 子句，則主體的安全性識別碼 (SID) 也會併入成為簽署程序的一部分。  
  
> [!CAUTION]
> 模組簽署只能用來授與權限，絕對不能用來拒絕或撤銷權限。  
  
 無法簽署內嵌資料表值函數。  
  
 您可以在 sys.crypt_properties 目錄檢視中，看到有關簽章的資訊。  
  
> [!WARNING]
>  當重新建立簽章的程序時，在原始批次的所有陳述式必須符合當重新建立批次。 如果批次中有任何部分不同 (即使是在空格或註解)，產生的簽章會有所不同。  
  
## <a name="countersignatures"></a>副署  
 當執行簽署的模組時，簽章會暫時新增至 SQL Token，但是如果此模組執行另一個模組或是此模組結束執行，簽章將會遺失。 副署是一種特殊形式的簽章。 副署簽章本身並不會授與任何權限，但是可允許在呼叫副署物件的期間，保留相同憑證或非對稱金鑰所做的簽章。  
  
 例如，假設使用者 Alice 呼叫 ProcSelectT1ForAlice 程序，此程序呼叫 procSelectT1 程序，後者是從資料表 T1 選取而來。 Alice 擁有 ProcSelectT1ForAlice 和 procSelectT1 的 EXECUTE 權限，但是沒有 T1 的 SELECT 權限，所以這整個鏈結中並未牽涉到任何擁有權鏈結。 Alice 無法存取資料表 T1，不論是直接存取還是透過 ProcSelectT1ForAlice 和 procSelectT1 的使用。 因為我們希望 Alice 一律使用 ProcSelectT1ForAlice 進行存取，所以我們不想要授與其執行 procSelectT1 的權限。 我們該怎麼完成呢？  
  
-   如果我們簽署 procSelectT1，好讓 procSelectT1 可以存取 T1，則 Alice 就可以直接叫用 procSelectT1，而且他不必呼叫 ProcSelectT1ForAlice。  
  
-   我們可拒絕將 procSelectT1 的 EXECUTE 權限授與給 Alice，但 這樣 Alice 即無法透過 ProcSelectT1ForAlice 來呼叫 procSelectT1。
  
-   只簽署 ProcSelectT1ForAlice 是不可行的，因為在呼叫 procSelectT1 時將會遺失簽章。  
  
但是，透過用來簽署 ProcSelectT1ForAlice 的相同憑證副署 procSelectT1 時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在整個呼叫鏈結中保留簽章，而且允許存取 T1。 如果 Alice 嘗試直接呼叫 procSelectT1，他就無法存取 T1，因為副署不會授與任何權限。 例如，底下的 C 顯示這個範例的 [!INCLUDE[tsql](../../includes/tsql-md.md)]。  
  
## <a name="permissions"></a>權限  

需要物件的 ALTER 權限，以及憑證或非對稱金鑰的 CONTROL 權限。 如果相關聯的私密金鑰受到密碼保護，則使用者也必須有密碼。  
  
## <a name="examples"></a>範例  
  
### <a name="a-signing-a-stored-procedure-by-using-a-certificate"></a>A. 使用憑證來簽署預存程序

 下列範例以 `HumanResources.uspUpdateEmployeeLogin` 憑證簽署預存程序 `HumanResourcesDP`。  
  
```  
USE AdventureWorks2012;  
ADD SIGNATURE TO HumanResources.uspUpdateEmployeeLogin   
    BY CERTIFICATE HumanResourcesDP;  
GO  
```  
  
### <a name="b-signing-a-stored-procedure-by-using-a-signed-blob"></a>B. 使用簽署的 BLOB 來簽署預存程序

下列範例會建立新的資料庫，並建立要在此範例中使用的憑證。 此範例會建立及簽署簡單預存程序，並從 `sys.crypt_properties` 中擷取 BLOB 簽章。 然後卸除及重新加入簽章。 這個範例會使用 WITH SIGNATURE 語法簽署此程序。  
  
```  
CREATE DATABASE TestSignature ;  
GO  
USE TestSignature ;  
GO  
-- Create a CERTIFICATE to sign the procedure.  
CREATE CERTIFICATE cert_signature_demo   
    ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'  
    WITH SUBJECT = 'ADD SIGNATURE demo';  
GO  
-- Create a simple procedure.  
CREATE PROC [sp_signature_demo]  
AS  
    PRINT 'This is the content of the procedure.' ;  
GO  
-- Sign the procedure.  
ADD SIGNATURE TO [sp_signature_demo]   
    BY CERTIFICATE [cert_signature_demo]   
    WITH PASSWORD = 'pGFD4bb925DGvbd2439587y' ;  
GO  
-- Get the signature binary BLOB for the sp_signature_demo procedure.  
SELECT cp.crypt_property  
    FROM sys.crypt_properties AS cp  
    JOIN sys.certificates AS cer  
        ON cp.thumbprint = cer.thumbprint  
    WHERE cer.name = 'cert_signature_demo' ;  
GO  
```  
  
 每次當您建立程序時，這個陳述式傳回的 `crypt_property` 簽章都會不同。 請記下結果，稍後可用於此範例中。 以此範例為例，示範的結果如下：`0x831F5530C86CC8ED606E5BC2720DA835351E46219A6D5DE9CE546297B88AEF3B6A7051891AF3EE7A68EAB37CD8380988B4C3F7469C8EABDD9579A2A5C507A4482905C2F24024FFB2F9BD7A953DD5E98470C4AA90CE83237739BB5FAE7BAC796E7710BDE291B03C43582F6F2D3B381F2102EEF8407731E01A51E24D808D54B373`。  
  
```  
-- Drop the signature so that it can be signed again.  
DROP SIGNATURE FROM [sp_signature_demo]   
    BY CERTIFICATE [cert_signature_demo];  
GO  
-- Add the signature. Use the signature BLOB obtained earlier.  
ADD SIGNATURE TO [sp_signature_demo]   
    BY CERTIFICATE [cert_signature_demo]  
    WITH SIGNATURE = 0x831F5530C86CC8ED606E5BC2720DA835351E46219A6D5DE9CE546297B88AEF3B6A7051891AF3EE7A68EAB37CD8380988B4C3F7469C8EABDD9579A2A5C507A4482905C2F24024FFB2F9BD7A953DD5E98470C4AA90CE83237739BB5FAE7BAC796E7710BDE291B03C43582F6F2D3B381F2102EEF8407731E01A51E24D808D54B373 ;  
GO  
```  
  
### <a name="c-accessing-a-procedure-using-a-countersignature"></a>C. 使用副署簽章存取程序

下列範例示範副署簽章如何控制物件的存取。  
  
```  
-- Create tesT1 database  
CREATE DATABASE testDB;  
GO  
USE testDB;  
GO  
-- Create table T1  
CREATE TABLE T1 (c varchar(11));  
INSERT INTO T1 VALUES ('This is T1.');  
  
-- Create a TestUser user to own table T1  
CREATE USER TestUser WITHOUT LOGIN;  
ALTER AUTHORIZATION ON T1 TO TestUser;  
  
-- Create a certificate for signing  
CREATE CERTIFICATE csSelectT  
  ENCRYPTION BY PASSWORD = 'SimplePwd01'  
  WITH SUBJECT = 'Certificate used to grant SELECT on T1';  
CREATE USER ucsSelectT1 FROM CERTIFICATE csSelectT;  
GRANT SELECT ON T1 TO ucsSelectT1;  
  
-- Create a principal with low privileges  
CREATE LOGIN Alice WITH PASSWORD = 'SimplePwd01';  
CREATE USER Alice;  
  
-- Verify Alice cannoT1 access T1;  
EXECUTE AS LOGIN = 'Alice';  
    SELECT * FROM T1;  
REVERT;  
  
-- Create a procedure that directly accesses T1  
CREATE PROCEDURE procSelectT1 AS  
BEGIN  
    PRINT 'Now selecting from T1...';  
    SELECT * FROM T1;  
END;  
GO  
GRANT EXECUTE ON procSelectT1 to public;  
  
-- Create special procedure for accessing T1  
CREATE PROCEDURE  procSelectT1ForAlice AS  
BEGIN  
   IF USER_ID() <> USER_ID('Alice')  
    BEGIN  
        PRINT 'Only Alice can use this.';  
        RETURN  
    END  
   EXEC procSelectT1;  
END;  
GO;  
GRANT EXECUTE ON procSelectT1ForAlice TO PUBLIC;  
  
-- Verify procedure works for a sysadmin user  
EXEC procSelectT1ForAlice;  
  
-- Alice still can't use the procedure yet  
EXECUTE AS LOGIN = 'Alice';  
    EXEC procSelectT1ForAlice;  
REVERT;  
  
-- Sign procedure to grant it SELECT permission  
ADD SIGNATURE TO procSelectT1ForAlice BY CERTIFICATE csSelectT   
WITH PASSWORD = 'SimplePwd01';  
  
-- Counter sign proc_select_t, to make this work  
ADD COUNTER SIGNATURE TO procSelectT1 BY CERTIFICATE csSelectT   
WITH PASSWORD = 'SimplePwd01';  
  
-- Now the proc works.   
-- Note that calling procSelectT1 directly still doesn't work  
EXECUTE AS LOGIN = 'Alice';  
    EXEC procSelectT1ForAlice;  
    EXEC procSelectT1;  
REVERT;  
  
-- Cleanup  
USE master;  
GO  
DROP DATABASE testDB;  
DROP LOGIN Alice;  
  
```  
  
## <a name="see-also"></a>另請參閱

- [sys.crypt_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-crypt-properties-transact-sql.md)
- [DROP SIGNATURE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-signature-transact-sql.md)
