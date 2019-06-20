---
title: 開始使用 Linux 上的 SQL Server 安全性 |Microsoft 文件
description: 本文說明一般的安全性動作。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ecc72850-8b01-492e-9a27-ec817648f0e0
ms.openlocfilehash: 655aebb0c07c812a7aa6c81e7c7033d85e8b7ce2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66705202"
---
# <a name="walkthrough-for-the-security-features-of-sql-server-on-linux"></a>在 Linux 上的 SQL Server 的安全性功能的逐步解說

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

如果您是剛接觸 SQL Server 的 Linux 使用者時，下列工作會引導您完成一些安全性工作。 這些不是唯一或特定 Linux，但它有助於讓您了解區域以進一步調查。 在每個範例中，會提供該區域的深入文件的連結。

> [!NOTE]
>  下列範例會使用**AdventureWorks2014**範例資料庫。 如需有關如何取得並安裝這個範例資料庫的指示，請參閱 <<c0> [ 從 Windows 的 SQL Server 資料庫還原到 Linux](sql-server-linux-migrate-restore-database.md)。


## <a name="create-a-login-and-a-database-user"></a>建立登入和資料庫使用者 

授與其他人所建立的登入在 master 資料庫中使用的 SQL Server 存取[CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md)陳述式。 例如：

```
CREATE LOGIN Larry WITH PASSWORD = '************';  
```

> [!NOTE]
>  在前一個命令中，永遠使用強式密碼取代星號。

登入可以連接到 SQL Server，並具有 master 資料庫 （具有有限的權限） 存取。 若要連接至使用者資料庫，登入必須在資料庫層級，呼叫資料庫使用者對應的身分識別。 使用者只適用於每個資料庫，而且必須授與他們存取的每個資料庫中個別建立。 下列範例會將您移至 AdventureWorks2014 資料庫，並接著會使用[CREATE USER](../t-sql/statements/create-user-transact-sql.md)陳述式來建立名為 Larry 與名為 Larry 登入相關聯的使用者。 登入和使用者相關 （彼此對應），但它們是不同的物件。 登入是伺服器層級原則。 使用者是資料庫層級主體。

```
USE AdventureWorks2014;
GO
CREATE USER Larry;
GO
```

- SQL Server 系統管理員帳戶可以連接到任何資料庫，而且可以建立多個登入和使用者在任何資料庫中。  
- 當有人建立資料庫時，它們成為資料庫擁有者，可以連接至該資料庫。 資料庫擁有者可以建立更多使用者。

稍後您可以授權其他登入，以便建立更多的登入，授與他們`ALTER ANY LOGIN`權限。 在資料庫內，您可以授權其他使用者授與它們建立更多使用者`ALTER ANY USER`權限。 例如：   

```
GRANT ALTER ANY LOGIN TO Larry;   
GO   
   
USE AdventureWorks2014;   
GO   
GRANT ALTER ANY USER TO Jerry;    
GO   
```

登入 Larry 現在可以建立多個登入和使用者 Jerry 可以建立更多使用者。


## <a name="granting-access-with-least-privileges"></a>以最低權限的存取權授與

系統管理員和資料庫擁有者帳戶，將會連接至使用者資料庫的第一個人。 不過這些使用者會在資料庫上擁有可用的所有權限。 這是更多的權限的大部分使用者應該擁有比。 

當您剛開始使用時，您就可以使用內建指派權限的某些一般分類*固定資料庫角色*。 比方說，`db_datareader`固定的資料庫角色可以讀取所有的資料表，在資料庫中，但不做任何變更。 使用授與固定的資料庫角色的成員資格[ALTER ROLE](../t-sql/statements/alter-role-transact-sql.md)陳述式。 下列範例會將使用者新增`Jerry`至`db_datareader`固定的資料庫角色。   
   
```   
USE AdventureWorks2014;   
GO   
   
ALTER ROLE db_datareader ADD MEMBER Jerry;   
```   

如需固定的資料庫角色的清單，請參閱 <<c0> [ 資料庫層級角色](../relational-databases/security/authentication-access/database-level-roles.md)。

稍後，當您準備好要設定更精確地存取您的資料 （強烈建議），建立您自己使用的使用者定義資料庫角色[CREATE ROLE](../t-sql/statements/create-role-transact-sql.md)陳述式。 然後，將特定的細微權限指派給您的自訂角色。

例如，下列陳述式建立名為的資料庫角色`Sales`，授與`Sales`分組的能力，請參閱、 更新和刪除資料列`Orders`資料表，然後再將使用者加入`Jerry`到`Sales`角色。   
   
```   
CREATE ROLE Sales;   
GRANT SELECT ON Object::Sales TO Orders;   
GRANT UPDATE ON Object::Sales TO Orders;   
GRANT DELETE ON Object::Sales TO Orders;   
ALTER ROLE Sales ADD MEMBER Jerry;   
```   

For more information about the permission system, see [Getting Started with Database Engine Permissions](../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).


## Configure row-level security  

[Row-Level Security](../relational-databases/security/row-level-security.md) enables you to restrict access to rows in a database based on the user executing a query. This feature is useful for scenarios like ensuring that customers can only access their own data or that workers can only access data that is pertinent to their department.   

The following steps walk through setting up two Users with different row-level access to the `Sales.SalesOrderHeader` table. 

Create two user accounts to test the row level security:    
   
```   
USE AdventureWorks2014;   
GO   
   
CREATE USER Manager WITHOUT LOGIN;     
   
CREATE USER SalesPerson280 WITHOUT LOGIN;    
```   

Grant read access on the `Sales.SalesOrderHeader` table to both users:    
   
```   
GRANT SELECT ON Sales.SalesOrderHeader TO Manager;      
GRANT SELECT ON Sales.SalesOrderHeader TO SalesPerson280;    
```   
   
Create a new schema and inline table-valued function. The function returns 1 when a row in the `SalesPersonID` column matches the ID of a `SalesPerson` login or if the user executing the query is the Manager user.   
   
```     
CREATE SCHEMA Security;   
GO   
   
CREATE FUNCTION Security.fn_securitypredicate(@SalesPersonID AS int)     
    RETURNS TABLE   
WITH SCHEMABINDING   
AS     
   RETURN SELECT 1 AS fn_securitypredicate_result    
WHERE ('SalesPerson' + CAST(@SalesPersonId as VARCHAR(16)) = USER_NAME())     
    OR (USER_NAME() = 'Manager');    
```   

Create a security policy adding the function as both a filter and a block predicate on the table:  

```
建立安全性原則 SalesFilter   
ADD FILTER PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  在 Sales.SalesOrderHeader，   
ADD BLOCK PREDICATE Security.fn_securitypredicate(SalesPersonID)    
  在 Sales.SalesOrderHeader   
WITH (STATE = ON);   
```

Execute the following to query the `SalesOrderHeader` table as each user. Verify that `SalesPerson280` only sees the 95 rows from their own sales and that the `Manager` can see all the rows in the table.  

```    
EXECUTE AS USER = 'SalesPerson280';   
SELECT * FROM Sales.SalesOrderHeader;    
還原; 
 
EXECUTE AS USER = 'Manager';   
SELECT * FROM Sales.SalesOrderHeader;   
還原;   
```
 
Alter the security policy to disable the policy.  Now both users can access all rows. 

```
改變安全性原則 SalesFilter   
WITH (STATE = OFF);    
``` 


## Enable dynamic data masking

[Dynamic Data Masking](../relational-databases/security/dynamic-data-masking.md) enables you to limit the exposure of sensitive data to users of an application by fully or partially masking certain columns. 

Use an `ALTER TABLE` statement to add a masking function to the `EmailAddress` column in the `Person.EmailAddress` table: 
 
```
USE AdventureWorks2014; GO ALTER TABLE Person.EmailAddress     ALTER COLUMN EmailAddress    
ADD MASKED WITH (FUNCTION = 'email()');
``` 
 
Create a new user `TestUser` with `SELECT` permission on the table, then execute a query as `TestUser` to view the masked data:   

```  
建立使用者 TestUser 沒有登入;   
GRANT SELECT ON Person.EmailAddress TO TestUser;    
 
EXECUTE AS USER = 'TestUser';   
SELECT EmailAddressID, EmailAddress FROM Person.EmailAddress;       
還原;    
```
 
Verify that the masking function changes the email address in the first record from:
  
|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |ken0@adventure-works.com |    
 
into 

|EmailAddressID |EmailAddress |  
|----|---- |   
|1 |kXXX@XXXX.com |   


## Enable Transparent Data Encryption

One threat to your database is the risk that someone will steal the database files off of your hard-drive. This could happen with an intrusion that gets elevated access to your system, through the actions of a problem employee, or by theft of the computer containing the files (such as a laptop).

Transparent Data Encryption (TDE) encrypts the data files as they are stored on the hard drive. The master database of the SQL Server database engine has the encryption key, so that the database engine can manipulate the data. The database files cannot be read without access to the key. High-level administrators can manage, backup, and recreate the key, so the database can be moved, but only by selected people. When TDE is configured, the `tempdb` database is also automatically encrypted. 

Since the Database Engine can read the data, Transparent Data Encryption does not protect against unauthorized access by administrators of the computer who can directly read memory, or access SQL Server through an administrator account.

### Configure TDE

- Create a master key
- Create or obtain a certificate protected by the master key
- Create a database encryption key and protect it by the certificate
- Set the database to use encryption

Configuring TDE requires `CONTROL` permission on the master database and `CONTROL` permission on the user database. Typically an administrator configures TDE. 

The following example illustrates encrypting and decrypting the `AdventureWorks2014` database using a certificate installed on the server named `MyServerCert`.


```
USE master;  
GO  

CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**********';  
GO  

CREATE CERTIFICATE MyServerCert WITH SUBJECT = 'My Database Encryption Key Certificate';  
GO  

USE AdventureWorks2014;   GO
  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_256  
ENCRYPTION BY SERVER 憑證 MyServerCert;  
GO
  
ALTER DATABASE AdventureWorks2014  
設定加密   
```

To remove TDE, execute `ALTER DATABASE AdventureWorks2014 SET ENCRYPTION OFF;`   

The encryption and decryption operations are scheduled on background threads by SQL Server. You can view the status of these operations using the catalog views and dynamic management views in the list that appears later in this topic.   

> [!WARNING]
>  Backup files of databases that have TDE enabled are also encrypted by using the database encryption key. As a result, when you restore these backups, the certificate protecting the database encryption key must be available. This means that in addition to backing up the database, you have to make sure that you maintain backups of the server certificates to prevent data loss. Data loss will result if the certificate is no longer available. For more information, see [SQL Server Certificates and Asymmetric Keys](../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  

For more information about TDE, see [Transparent Data Encryption (TDE)](../relational-databases/security/encryption/transparent-data-encryption-tde.md).   


## Configure backup encryption
SQL Server has the ability to encrypt the data while creating a backup. By specifying the encryption algorithm and the encryptor (a certificate or asymmetric key) when creating a backup, you can create an encrypted backup file.    
  
> [!WARNING]  
>  It is very important to back up the certificate or asymmetric key, and preferably to a different location than the backup file it was used to encrypt. Without the certificate or asymmetric key, you cannot restore the backup, rendering the backup file unusable. 
 
 
The following example creates a certificate, and then creates a backup protected by the certificate.
```
使用主版; 移 建立憑證 BackupEncryptCert 主體 = '資料庫備份;' 請備份資料庫 [AdventureWorks2014] 磁碟 = N'/var/opt/mssql/backups/AdventureWorks2014.bak'  
取代所有提及的  
  壓縮，  
  ENCRYPTION   
   (  
   ALGORITHM = AES_256,  
   SERVER CERTIFICATE = BackupEncryptCert  
   ),  
  STATS = 10  
GO  
```

For more information, see [Backup Encryption](../relational-databases/backup-restore/backup-encryption.md).


## Next steps

For more information about the security features of SQL Server, see [Security Center for SQL Server Database Engine and Azure SQL Database](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).
