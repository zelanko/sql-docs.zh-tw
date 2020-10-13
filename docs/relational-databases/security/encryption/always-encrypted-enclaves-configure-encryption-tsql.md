---
description: 使用 Transact-SQL 就地設定資料行加密
title: 使用 Transact-SQL 就地設定資料行加密 | Microsoft Docs
ms.custom: ''
ms.date: 10/10/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 90bb710e57e87bfb6bf86f4ae0543329a4500940
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91863649"
---
# <a name="configure-column-encryption-in-place-with-transact-sql"></a>使用 Transact-SQL 就地設定資料行加密
[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

本文描述如何使用具有安全記憶體保護區的 Always Encrypted 來搭配 [ALTER TABLE 陳述式](../../../odbc/microsoft/alter-table-statement.md)/`ALTER COLUMN` 陳述式，就地對資料行執行密碼編譯作業。 如需就地加密和一般必要條件的基本資訊，請參閱[使用具有安全記憶體保護區的 Always Encrypted 就地設定資料行加密](always-encrypted-enclaves-configure-encryption.md)。

您可以使用 `ALTER TABLE` 或 `ALTER COLUMN` 陳述式來設定資料行的目標加密設定。 當您執行陳述式時，伺服器端安全記憶體保護區會根據陳述式內資料行定義中所指定目前和目標加密設定來加密、重新加密或解密資料行中儲存的資料。 
- 如果資料行目前未加密，則當您在資料行定義中指定 `ENCRYPTED WITH` 子句時，就會將其加密。
- 如果資料行目前已加密，則當您未在資料行定義中指定 `ENCRYPTED WITH` 子句時，就會將其解密 (轉換成純文字資料行)。
- 如果資料行目前已加密，則當您指定 `ENCRYPTED WITH` 子句，且所指定資料行加密類型或資料行加密金鑰與目前使用的加密類型或資料行加密金鑰不同，就會重新加密該資料行。 

> [!NOTE]
> 除了將資料行變更為 `NULL` 或 `NOT NULL`，或變更定序以外，您無法將密碼編譯作業與單一 `ALTER TABLE`/`ALTER COLUMN` 陳述式中的其他變更結合。 例如，您無法加密資料行，同時在單一 `ALTER TABLE`/`ALTER COLUMN` Transact-SQL 陳述式中變更資料行的資料類型。 請使用兩個個別的陳述式。

作為使用伺服器端安全記憶體保護區的任何查詢，就地觸發加密的 `ALTER TABLE`/`ALTER COLUMN` 陳述式必須透過已啟用 Always Encrypted 和記憶體保護區計算的連線來傳送。 

本文的其餘部分將描述如何從 SQL Server Management Studio 使用 `ALTER TABLE`/`ALTER COLUMN` 陳述式來觸發就地加密。 或者，您也可以從應用程式發出 `ALTER TABLE`/`ALTER COLUMN`。 

> [!NOTE]
> 目前，SSMS 以外的工具 (包括 SqlServer PowerShell 模組中的 [Invoke-Sqlcmd](/powershell/module/sqlserver/invoke-sqlcmd) Cmdlet 以及 [sqlcmd](../../../tools/sqlcmd-utility.md)) 不支援使用 `ALTER TABLE`/`ALTER COLUMN` 進行就地密碼編譯作業。

## <a name="perform-in-place-encryption-with-transact-sql-in-ssms"></a>請使用 SSMS 中的 Transact-SQL 執行就地加密
### <a name="pre-requisites"></a>必要條件
- [使用具有安全記憶體保護區的 Always Encrypted 就地設定資料行加密](always-encrypted-enclaves-configure-encryption.md)中所述必要條件。
- SQL Server Management Studio 18.3 或更高版本。

### <a name="steps"></a>步驟
1. 使用 Always Encrypted 和資料庫連接中所啟用的記憶體保護區計算來開啟查詢視窗。 如需詳細資料，請參閱[針對資料庫連接啟用和停用 Always Encrypted](always-encrypted-query-columns-ssms.md#en-dis)。
2. 在查詢視窗中，發出 `ALTER TABLE`/`ALTER COLUMN` 陳述式，並在 `ENCRYPTED WITH` 子句中指定已啟用記憶體保護區的資料行加密金鑰。 如果您的資料行是字串資料行 (例如，`char`、`varchar`、`nchar`、`nvarchar`)，則您也可能需要將定序變更為 BIN2 定序。 
    
    > [!NOTE]
    > 如果您的資料行主要金鑰儲存至 Azure Key Vault，則系統可能會提示您登入 Azure。

3. 清除會存取資料表的所有批次和預存程序的計畫快取，以重新整理參數加密資訊。 
 
    ```sql
    ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
    ```
    > [!NOTE]
    > 如果您未從快取中移除受影響查詢的計畫，則加密後的第一次執行查詢可能會失敗。

    > [!NOTE]
    > 使用 `ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE` 或 `DBCC FREEPROCCACHE` 小心地清除計畫快取，因為它可能會導致暫時性的查詢效能降低。 若要將清除快取的負面影響降到最低，您可以選擇性地僅移除受影響查詢的計畫。

4.  呼叫 [sp_refresh_parameter_encryption](../../system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md) 來針對在 [sys.parameters](../..//system-catalog-views/sys-parameters-transact-sql.md) 中保存且因對資料行加密而可能已經失效的每個模組 (預存程序、函式、檢視、觸發程序) 的參數更新中繼資料。

### <a name="examples"></a>範例
#### <a name="encrypting-a-column-in-place"></a>就地加密資料行
下列範例假設：
- `CEK1` 是已啟用記憶體保護區的資料行加密金鑰。
- `SSN` 資料行是純文字，且目前使用 Latin1、非 BIN2 定序 (例如，`Latin1_General_CI_AI_KS_WS`) 之類的預設資料庫定序。

此陳述式會使用隨機化加密和已啟用記憶體保護區的資料行加密金鑰來就地加密 `SSN` 資料行。 它也會將預設資料庫定序覆寫為對應 (在相同的字碼頁中) BIN2 定序。

作業會在線上執行 (`ONLINE = ON`)。 另請注意，`ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE` 呼叫可重新建立受資料表結構描述變更所影響的查詢計畫。

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char] COLLATE Latin1_General_BIN2
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
WITH
(ONLINE = ON);
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

#### <a name="re-encrypt-a-column-in-place-to-change-encryption-type"></a>就地重新加密資料行以變更加密類型
下列範例假設：
- 使用確定性加密和已啟用記憶體保護區的資料行加密金鑰 `CEK1` 來加密 `SSN` 資料行。
- 目前的定序 (設定於資料行層級) 為 `Latin1_General_BIN2`。

下列陳述式會使用隨機化加密和相同的金鑰 (`CEK1`) 來重新加密資料行

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) COLLATE Latin1_General_BIN2
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1]
, ENCRYPTION_TYPE = Randomized
, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL;
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

#### <a name="re-encrypt-a-column-in-place-to-rotate-a-column-encryption-key"></a>就地重新加密資料行以輪替資料行加密金鑰
下列範例假設：
- 使用隨機化加密和已啟用記憶體保護區的資料行加密金鑰 `CEK1` 來加密 `SSN` 資料行。
- `CEK2` 是已啟用記憶體保護區的資料行加密金鑰 (不同於 `CEK1`)。
- 目前的定序 (設定於資料行層級) 為 `Latin1_General_BIN2`。

下列陳述式會使用 `CEK2` 來重新加密資料行。

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) COLLATE Latin1_General_BIN2
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK2]
, ENCRYPTION_TYPE = Randomized
, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL;
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```
#### <a name="decrypt-a-column-in-place"></a>就地解密資料行
下列範例假設：
- 使用已啟用記憶體保護區的資料行加密金鑰來加密 `SSN` 資料行。
- 目前的定序 (設定於資料行層級) 為 `Latin1_General_BIN2`。

下列陳述式會解密資料行 (並保持定序不變；或者，舉例來說，您可以選擇在相同陳述式中將定序變更為非 BIN2 定序)。

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) COLLATE Latin1_General_BIN2
WITH (ONLINE = ON);
GO
ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
GO
```

## <a name="next-steps"></a>後續步驟
- [使用具有安全記憶體保護區的 Always Encrypted 查詢資料行](always-encrypted-enclaves-query-columns.md)
- [使用具有安全記憶體保護區的 Always Encrypted 在資料行上建立及使用索引](always-encrypted-enclaves-create-use-indexes.md)
- [使用具有安全記憶體保護區的 Always Encrypted 開發應用程式](always-encrypted-enclaves-client-development.md)

## <a name="see-also"></a>另請參閱  
- [使用具有安全記憶體保護區的 Always Encrypted 就地設定資料行加密](always-encrypted-enclaves-configure-encryption.md)
- [為現有加密資料行啟用具有安全記憶體保護區的 Always Encrypted](always-encrypted-enclaves-enable-for-encrypted-columns.md)
- [教學課程：使用 SSMS，開始使用具有安全記憶體保護區的 Always Encrypted](../tutorial-getting-started-with-always-encrypted-enclaves.md)