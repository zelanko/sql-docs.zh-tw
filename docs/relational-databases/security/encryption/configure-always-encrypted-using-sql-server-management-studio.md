---
title: "使用 SQL Server Management Studio 設定 Always Encrypted | Microsoft Docs"
ms.custom: 
ms.date: 11/30/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.SWB.COLUMNMASTERKEY.PAGE.F1
- SQL13.SWB.COLUMNENCRYPTIONKEY.PAGE.F1
- SQL13.SWB.COLUMNMASTERKEY.ROTATION.F1
helpviewer_keywords:
- Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 80c832db0ffdb9a3666b60a19fdf11a01750b2e1
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="configure-always-encrypted-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 設定永遠加密
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

本文所說明的工作是有關設定永遠加密以及管理搭配使用永遠加密與 [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx) 的資料庫。

當您使用 SSMS 設定永遠加密時，SSMS 會同時處理永遠加密金鑰和敏感性資料，因此金鑰和資料會以純文字形式出現在 SSMS 處理序內。 因此，請務必在安全的電腦上執行 SSMS。 如果您的資料庫裝載在 SQL Server 上，請確定在與裝載 SQL Server 執行個體不同的電腦上執行 SSMS。 因為永遠加密的主要目標是為了確保已加密的敏感性資料安全無虞，即使資料庫系統遭到入侵亦然，所以在 SQL Server 電腦上執行處理金鑰或敏感性資料的 PowerShell 指令碼，可能會降低或損害此功能的優點。 如需其他建議，請參閱 [金鑰管理的安全性考量](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md#SecurityForKeyManagement)。

SSMS 不支援下列兩者之間的角色隔離：管理資料庫的人員 (DBA) 與管理密碼編譯密碼且有權存取純文字資料的人員 (安全性系統管理員和/或應用程式系統管理員)。 如果您的組織強制執行角色隔離，則應該使用 PowerShell 設定永遠加密。 如需詳細資訊，請參閱 [永遠加密的金鑰管理概觀](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md) 和 [使用 PowerShell 設定永遠加密](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)。

## <a name="configuring-always-encrypted-using-the-always-encrypted-wizard"></a>使用永遠加密精靈設定永遠加密

[[永遠加密精靈](../../../relational-databases/security/encryption/always-encrypted-wizard.md)] 是一個功能強大的工具，可讓您設定所選取資料庫資料行的所需加密組態。 根據目前永遠加密組態和所要的目標組態，精靈可以加密資料行、將其解密 (移除加密) 或重新加密 (例如，使用新的資料行加密金鑰，或與針對資料行設定的目前類型不同的加密類型)。 在精靈的單一執行中，可以設定多個資料行。

如果您尚未佈建永遠加密的任何金鑰，精靈將會自動產生金鑰。 您只需要挑選資料行主要金鑰的金鑰存放區：Windows 憑證存放區或 Azure 金鑰保存庫。 精靈將自動產生資料庫中金鑰和其中繼資料物件的名稱。 如果您需要深入控制如何佈建您的金鑰 (以及含有資料行主要金鑰之金鑰存放區的更多選擇)，則可以先使用 [新增資料行主要金鑰] **** 和 [新增資料行加密金鑰] **** 對話方塊 (如下所述) 來佈建金鑰，再啟動精靈。 在 [永遠加密精靈] 中，您接著可以挑選現有的資料行加密金鑰。

如需如何使用精靈的詳細資訊，請參閱  [永遠加密精靈](../../../relational-databases/security/encryption/always-encrypted-wizard.md)。

## <a name="querying-encrypted-columns"></a>查詢加密資料行

本節說明如何：   
-   擷取加密資料行中儲存的加密文字值。   
-   擷取加密資料行中儲存的純文字值。   
-   傳送目標為加密資料行的純文字值 (例如，在 `INSERT` 或 `UPDATE` 陳述式中，以及在 `WHERE` 陳述式中做為 `SELECT` 子句的查閱參數)。   

### <a name="retrieving-ciphertext-values-stored-in-encrypted-columns"></a>擷取加密資料行中儲存的加密文字值    

擷取加密資料行的值做為加密文字 (而不需將值解密)：
1.    確定會針對您從中執行 `SELECT` 查詢的 [查詢編輯器] 視窗的資料庫連接停用 Always Encrypted。 請參閱下方的 [針對資料庫連接啟用和停用 Always Encrypted](#en-dis) 。      
2.    執行 `SELECT` 查詢。 從加密資料行擷取的任何資料都將當做二進位 (加密) 值來傳回。   

*範例*   
假設 `SSN` 是 `Patients` 資料表中的加密資料行，如果已針對資料庫連接停用 Always Encrypted，以下所示的查詢將擷取二進位的加密文字值。   

![always-encrypted-ciphertext](../../../relational-databases/security/encryption/media/always-encrypted-ciphertext.png)
 
### <a name="retrieving-plaintext-values-stored-in-encrypted-columns"></a>擷取加密資料行中儲存的純文字值    

擷取加密資料行的值做為純文字 (以便將值解密)：   
1.    確定會針對您從中執行 `SELECT` 查詢的 [查詢編輯器] 視窗的資料庫連接啟用 Always Encrypted。 這將指示 .NET Framework Data Provider for SQL Server (由 SSMS所使用)，將從加密資料行擷取的資料解密。 請參閱下方的 [針對資料庫啟用和停用 Always Encrypted](#en-dis) 。
2.    確定您可以存取針對加密資料行設定的所有資料行主要金鑰。 例如，如果您的資料行主要金鑰是一個憑證，您就需要確定憑證是部署於執行 SSMS 的電腦上。 或者，如果您的資料行主要金鑰是儲存在 Azure 金鑰保存庫中的金鑰，則需確定您擁有存取金鑰的權限 (此外，系統可能會提示您登入 Azure)。
3.    執行 `SELECT` 查詢。 從加密資料行擷取的任何資料將會以純文字傳回，來做為原始資料類型的值。   

*範例*   
假設 SSN 是 `char(11)` 資料表中加密的 `Patients` 資料行，如果已針對資料庫連接啟用 Always Encrypted，而且您有權存取針對 `SSN` 資料行設定的資料行主要金鑰，則以下所示的查詢將傳回純文字值。   

![always-encrypted-plaintext](../../../relational-databases/security/encryption/media/always-encrypted-plaintext.png)
 
### <a name="sending-plaintext-values-targeting-encrypted-columns"></a>傳送目標為加密資料行的純文字值       

執行查詢以傳送目標為加密資料行的值，例如，利用儲存於加密資料行中的值來插入、更新或據以篩選的查詢：   
1.    確定會針對您從中執行 `SELECT` 查詢的 [查詢編輯器] 視窗的資料庫連接啟用 Always Encrypted。 這將指示 .NET Framework Data Provider for SQL Server (由 SSMS 所使用)，將目標為加密資料行且已參數化的 Transact-SQL 變數 (請參閱下方內容) 加密。 請參閱下方的 [針對資料庫啟用和停用 Always Encrypted](#en-dis) 。   
2.    確定您可以存取針對加密資料行設定的所有資料行主要金鑰。 例如，如果您的資料行主要金鑰是一個憑證，您就需要確定憑證是部署於執行 SSMS 的電腦上。 或者，如果您的資料行主要金鑰是儲存在 Azure 金鑰保存庫中的金鑰，則需確定您擁有存取金鑰的權限 (此外，系統可能會提示您登入 Azure)。   
3.    確定已針對 [查詢編輯器] 視窗啟用 [Always Encrypted 的參數化]。 (至少需要 SSMS 17.0 版。)宣告 Transact-SQL 變數，並使用您想要傳送 (插入、更新或據以篩選) 至資料庫的值來將它初始化。 如需詳細資訊，請參閱下方的 [Always Encrypted 的參數化](#param)。   
    >   [!NOTE]
    >   由於 Always Encrypted 支援一組有限的類型轉換子集，因此，在許多情況下，會要求 Transact-SQL 變數的資料類型與其設定為目標的目標資料庫資料行的類型相同。   
4.    執行查詢以將 Transact-SQL 變數的值傳送至資料庫。 SSMS 會將變數轉換為查詢參數，而它會在將值傳送至資料庫之前，先進行加密。   

*範例*   
假設 `SSN` 是 `char(11)` 資料表中加密的 `Patients` 資料行，以下指令碼將嘗試在 SSN 資料行中尋找包含 `'795-73-9838'` 的資料列，並傳回 `LastName` 資料行的值，但前提是已針對資料庫連線啟用 Always Encrypted、已針對 [查詢編輯器] 視窗啟用 [Always Encrypted 的參數化]，而且您有權存取針對 `SSN` 資料行設定的資料行主要金鑰。   

![always-encrypted-patients](../../../relational-databases/security/encryption/media/always-encrypted-patients.png)
 
### <a name="en-dis"></a> Enabling and disabling Always Encrypted for a database connection   

針對資料庫連線啟用和停用 Always Encrypted，會指示 .NET Framework Data Provider for SQL Server (SQL Server Management Studio 所使用) 明確地嘗試進行下列動作：   
-    將從加密資料行擷取以及查詢結果中傳回的任何值解密。   
-    將目標為加密資料庫資料行且已參數化的 Transact-SQL 變數的值加密。   
若要針對資料庫連接啟用 Always Encrypted，可在 [連接到伺服器] `Column Encryption Setting=Enabled`**對話方塊的 [其他屬性]****索引標籤中指定** 。    
若要針對資料庫連接停用 Always Encrypted，可指定 `Column Encryption Setting=Disabled` ，或者只需從 [連接到伺服器] **** 對話方塊的 [其他屬性] **** 索引標籤中移除 [資料行加密設定] **** 的設定 (預設值是 [已停用] ****)。   

>  [!TIP] 
>  在已針對現有的 [查詢編輯器] 視窗啟用和停用的 Always Encrypted 之間進行切換：   
>  1.    以滑鼠右鍵按一下 [查詢編輯器] 視窗中的任何位置。
>  2.    選取 [連接]**** > [變更連接...]****， 
>  3.    按一下 [選項]**** >>，
>  4.    選取 [其他屬性]**** 索引標籤，然後輸入 `Column Encryption Setting=Enabled` (以啟用 Always Encrypted 行為) 或移除設定 (以停用 Always Encrypted 行為)。   
>  5.    按一下 **[連接]**。   
   
### <a name="param"></a>Parameterization for Always Encrypted   
 
[Always Encrypted 的參數化] 是 SQL Server Management Studio 中的一項功能，可將 Transact-SQL 變數自動轉換為查詢參數 ([SqlParameter 類別](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx)的執行個體)。 (至少需要 SSMS 17.0 版。)這讓基礎的 .NET Framework Data Provider for SQL Server 能夠偵測目標為加密資料行的資料，並且在將這類資料傳送至資料庫之前，先進行加密。 
  
未啟用參數化時，.NET Framework Data Provider 會以非參數化的查詢傳遞您在 [查詢編輯器] 中撰寫的每一個陳述式。 如果查詢包含目標為加密資料行的常值或 Transact-SQL 變數，.NET Framework Data Provider for SQL Server 就無法在將查詢傳送至資料庫之前先偵測並加密它們。 如此一來，查詢將因 (純文字的常值 Transact-SQL 變數與加密資料行之間) 類型不符而導致失敗。 例如，假設 `SSN` 資料行已加密，下列查詢將因未啟用參數化而失敗。   

```tsql
DECLARE @SSN NCHAR(11) = '795-73-9838'
SELECT * FROM [dbo].[Patients]
WHERE [SSN] = @SSN
```

#### <a name="enablingdisabling-parameterization-for-always-encrypted"></a>啟用/停用 Always Encrypted 的參數化   


預設為停用 [Always Encrypted 的參數化]。    

針對目前的 [查詢編輯器] 視窗啟用/停用 [Always Encrypted 的參數化]：   
1.    從主功能表選取 [查詢] **** 。   
2.    選取 [查詢選項...]****。   
3.    瀏覽至 [執行]**** > [進階]****。   
4.    選取或取消選取 [啟用 Always Encrypted 的參數化]****。   
5.    按一下 **[確定]**。   

針對未來的 [查詢編輯器] 視窗啟用/停用 [Always Encrypted 的參數化]：   
1.    從主功能表選取 [工具] **** 。   
2.    選取 [選項...]****。   
3.    瀏覽至 [查詢執行]**** > [SQL Server]**** > [進階]****。   
4.    選取或取消選取 [啟用 Always Encrypted 的參數化]****。   
5.    按一下 **[確定]**。   

如果您執行查詢的 [查詢編輯器] 視窗會使用已啟用 Always Encrypted 的資料庫連接，但尚未針對 [查詢編輯器] 視窗啟用參數化，則系統將會提示您加以啟用。   
>   [!NOTE]   
>   [Always Encrypted 的參數化] 僅適用於使用已啟用 Always Encrypted 的資料庫連接的 [查詢編輯器] 視窗 (請參閱 [針對資料庫啟用和停用 Always Encrypted](#en-dis))。 如果 [查詢編輯器] 視窗使用尚未啟用 Always Encrypted 的資料庫連接，則不會將任何 Transact-SQL 變數參數化。   

#### <a name="how-parameterization-for-always-encrypted-works"></a>Always Encrypted 的參數化的運作方式   

如果已針對 [查詢編輯器] 視窗啟用 [Always Encrypted 的參數化] 和資料庫連接中的 Always Encrypted 行為，則 SQL Server Management Studio 會嘗試將 Transact-SQL 變數參數化，以符合下列必要條件的情況：    
- 在相同陳述式中宣告及初始化 (內嵌初始化)。 使用個別 `SET` 陳述式宣告的變數將不會參數化。   
- 使用單一常值初始化。 使用運算式 (包含任何運算子或函數) 初始化的變數將不會參數化。      

以下是 SQL Server Management Studio 將參數化的變數範例。   
```tsql
DECLARE @SSN char(11) = '795-73-9838';
   
DECLARE @BirthDate date = '19990104';
DECLARE @Salary money = $30000;
```

此外，以下是 SQL Server Management Studio 將不會嘗試參數化的一些變數範例：   
```tsql
DECLARE @Name nvarchar(50); --Initialization seperate from declaration
SET @Name = 'Abel';
   
DECLARE @StartDate date = GETDATE(); -- a function used instead of a literal
   
DECLARE @NewSalary money = @Salary * 1.1; -- an expression used instead of a literal
```
 
若要成功嘗試進行參數化：   
- 針對要參數化之變數初始化所使用的常值類型必須符合變數宣告中的類型。   
- 如果變數的宣告類型是日期類型或時間類型，就必須使用字串，以其中一個遵循 ISO 8601 規範的格式來初始化變數。   

以下是將產生參數化錯誤的 Transact-SQL 變數宣告範例：   
```tsql
DECLARE @BirthDate date = '01/04/1999' -- unsupported date format   
   
DECLARE @Number int = 1.1 -- the type of the literal does not match the type of the variable   
```
SQL Server Management Studio 會使用 Intellisense，來告知您哪些變數可以成功參數化，以及哪些參數化嘗試失敗 (與原因)。   

在 [查詢編輯器] 中，會以警告底線標示可成功參數化的變數宣告。 如果您將滑鼠停留在以警告底線標示的宣告陳述式上，您將會看到參數化程序的結果，包括所產生 [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) 物件 (變數要與其對應) 的主要屬性值： [SqlDbType](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.sqldbtype.aspx)、 [Size](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.size.aspx)、 [Precision](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.precision.aspx), [Scale](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.scale.aspx)、 [SqlValue](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.sqlvalue.aspx)。 您也可以在 [錯誤清單] **** 檢視的 [警告] **** 索引標籤中，查看已成功地參數化的所有變數的完整清單。 若要開啟 [錯誤清單] **** 檢視，從主功能表選取 [檢視] **** ，然後選取 [錯誤清單] ****。    

如果 SQL Server Management Studio 已嘗試將變數參數化，但參數化失敗，則將會以錯誤底線標示變數的宣告。 如果您將滑鼠停留在已使用錯誤底線標示的宣告陳述式上，您將會取得有關錯誤的結果。 您也可以在 [錯誤清單] **** 檢視的 [錯誤] **** 索引標籤中，查看所有變數的參數化錯誤的完整清單。 若要開啟 [錯誤清單] **** 檢視，從主功能表選取 [檢視] **** ，然後選取 [錯誤清單] ****。   

以下螢幕擷取畫面顯示六個變數宣告的範例。 SQL Server Management Studio 已成功將前三個變數參數化。 最後三個變數不符合參數化的必要條件情況，因此，SQL Server Management Studio 未嘗試將它們參數化 (未以任何方式標示它們的宣告)。   

![always-encrypted-parameter-warnings](../../../relational-databases/security/encryption/media/always-encrypted-parameter-warnings.png)
 
以下另一個示範顯示了兩個參數，其符合參數化的必要條件情況，但參數化嘗試因為變數未正確初始化而失敗。    
 
![always-encrypted-error](../../../relational-databases/security/encryption/media/always-encrypted-error.png)
 
>   [!NOTE]
>   由於 Always Encrypted 支援一組有限的類型轉換子集，因此，在許多情況下，會要求 Transact-SQL 變數的資料類型與其設定為目標的目標資料庫資料行的類型相同。 例如，假設 `SSN` 資料表中 `Patients` 資料行的類型是 `char(11)`，以下查詢將會失敗，因為 `@SSN` 變數的類型為 `nchar(11)`，不符合資料行的類型。   

```tsql
DECLARE @SSN nchar(11) = '795-73-9838'
SELECT * FROM [dbo].[Patients]
WHERE [SSN] = @SSN;
```

    Msg 402, Level 16, State 2, Line 5   
    The data types char(11) encrypted with (encryption_type = 'DETERMINISTIC', 
    encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'CEK_Auto1', 
    column_encryption_key_database_name = 'Clinic') collation_name = 'Latin1_General_BIN2' 
    and nchar(11) encrypted with (encryption_type = 'DETERMINISTIC', 
    encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'CEK_Auto1', 
    column_encryption_key_database_name = 'Clinic') are incompatible in the equal to operator.

>   [!NOTE]
>   未啟用參數化時，整個查詢 (包括類型轉換) 會在 SQL Server/Azure SQL Database 內部進行處理。 啟用參數化時，.NET Framework 會在 SQL Server Management Studio 內部執行一些類型轉換。 由於 .NET Framework 類型系統與 SQL Server 類型系統之間的差異 (例如某些類型 (例如浮點數) 的有效位數不同)，因此，已啟用參數化執行的查詢可以產生不同於未啟用參數化執行的查詢的結果。 

#### <a name="permissions"></a>Permissions      

若要針對加密資料行 (包括以加密文字擷取資料的查詢) 執行任何查詢，您需要資料庫中的 `VIEW ANY COLUMN MASTER KEY DEFINITION` 和 `VIEW ANY COLUMN ENCRYPTION KEY DEFINITION` 權限。   
除了上述權限，若要將任何查詢結果解密或加密任何查詢參數 (透過參數化 Transact-SQL 變數來產生)，您還需要權限來存取保護目標資料行的資料行主要金鑰：   
- **憑證存放區 - 本機電腦** 您必須具有當成資料行主要金鑰使用之憑證的 `Read` 權限，或為電腦上的系統管理員。   
- **Azure 金鑰保存庫** 您需要具有包含資料行主要金鑰之保存庫的 `get`、 `unwrapKey`和 verify 權限。   
- **金鑰存放區提供者 (CNG)** 必要權限和認證 (您在使用金鑰存放區或金鑰時可能收到提示) 取決於存放區和 KSP 組態。   
- **密碼編譯服務提供者 (CAPI)** 必要權限和認證 (您在使用金鑰存放區或金鑰時可能會收到提示) 取決於存放區和 CSP 組態。   

如需詳細資訊，請參閱 [建立及儲存資料行主要金鑰 (永遠加密)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)。


<a name="provisioncmk"></a>
## <a name="provisioning-column-master-keys-new-column-master-key"></a>佈建資料行主要金鑰 (新增資料行主要金鑰)

[新增資料行主要金鑰]**** 對話方塊可讓您產生資料行主要金鑰或挑選金鑰存放區中的現有金鑰，以及建立資料庫中所建立或所選取金鑰的資料行主要金鑰中繼資料。

1.    使用物件總管****，巡覽至資料庫下的 [安全性 > 永遠加密金鑰]**** 資料夾。
2.    以滑鼠右鍵按一下 [資料行主要金鑰]**** 資料夾，然後選取 [新增資料行主要金鑰]****。 
3.    在 [新增資料行主要金鑰] **** 對話方塊中，輸入資料行主要金鑰中繼資料物件的名稱。
4.    選取金鑰存放區︰
    - **憑證存放區 – 目前使用者** - 指出 Windows 憑證存放區中的目前使用者憑證存放區位置 (即個人存放區)。 
    - **憑證存放區 – 本機電腦** - 指出 Windows 憑證存放區中的本機電腦憑證存放區位置。 
    - **Azure 金鑰保存庫** - 您需要登入 Azure (按一下 [登入] ****)。 登入之後，就可以挑選其中一個 Azure 訂用帳戶和金鑰保存庫。
    - **金鑰存放區提供者 (CNG)** - 指出金鑰存放區，而金鑰存放區可透過實作新一代密碼編譯 (CNG) API 的金鑰存放區提供者 (KSP) 進行存取。 這種類型的存放區通常是硬體安全性模組 (HSM)。 在您選取此選項之後，需要挑選 KSP。 預設會選取 [ (Microsoft 軟體金鑰存放區提供者)]**** 。 如果您想要使用 HSM 中所儲存的資料行主要金鑰，請選取裝置的 KSP (它必須先安裝和設定於電腦上，您才能開啟對話方塊)。
    -    **密碼編譯服務提供者 (CAPI)** - 一種金鑰存放區，可透過實作密碼編譯 API (CAPI) 的密碼編譯服務提供者 (CSP) 進行存取。 這類存放區通常是硬體安全性模組 (HSM)。 在您選取此選項之後，需要挑選 CSP。  如果您想要使用 HSM 中所儲存的資料行主要金鑰，請選取裝置的 CSP (它必須先安裝和設定於電腦上，您才能開啟對話方塊)。
    
    >   [!NOTE]
    >   因為 CAPI 是已被取代的應用程式開發介面，所以預設會停用 [密碼編譯服務提供者 (CAPI)] 選項。 啟用方式是在 Windows 登錄的 **[HKEY_CURRENT_USER\Software\Microsoft\Microsoft SQL Server\sql13\Tools\Client\Always Encrypted]** 金鑰下建立 CAPI Provider Enabled DWORD 值，並將其設成 1。 除非您的金鑰存放區不支援 CNG，否則您應該使用 CNG，而非 CAPI。
   
    如需上述金鑰存放區的詳細資訊，請參閱 [建立及儲存資料行主要金鑰 (永遠加密)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)。

5.    挑選金鑰存放區中的現有金鑰，或按一下 [產生金鑰] **** 或 [產生憑證] **** 按鈕，以在金鑰存放區中建立金鑰。 
6.    按一下 [確定] **** ，新的金鑰即會顯示在清單中。 

SQL Server Management Studio 將會在資料庫中建立資料行主要金鑰的中繼資料。 此對話方塊的做法是產生和發出 [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) 陳述式。


<a name="provisioncek"></a> 
## <a name="provisioning-column-encryption-keys-new-column-encryption-key"></a>佈建資料行加密金鑰 (新增資料行加密金鑰)

[新增資料行加密金鑰] **** 對話方塊可讓您產生資料行加密金鑰、使用資料行主要金鑰進行加密，以及在資料庫中建立資料行加密金鑰中繼資料。

1.    使用物件總管 ****，巡覽至資料庫下的 [安全性]/[永遠加密金鑰] **** 資料夾。
2.    以滑鼠右鍵按一下 [資料行加密金鑰] **** 資料夾，然後選取 [新增資料行加密金鑰] ****。 
3.    在 [新增資料行加密金鑰] **** 對話方塊中，輸入資料行加密金鑰中繼資料物件的名稱。
4.    選取代表資料庫中資料行主要金鑰的中繼資料物件。
5.    按一下 **[確定]**。 


SQL Server Management Studio 將會產生新的資料行加密金鑰，接著會擷取您從資料庫選取之資料行主要金鑰的中繼資料。 SQL Server Management Studio 接著將使用資料行主要金鑰中繼資料來連絡包含資料行主要金鑰的金鑰存放區，並加密資料行加密金鑰。 最後，將會在資料庫中建立新資料行加密金鑰的中繼資料。 此對話方塊的做法是產生和發出 [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md) 陳述式。

### <a name="permissions"></a>Permissions

您需要具有資料庫中的 *ALTER ANY ENCRYPTION MASTER KEY* 和 *VIEW ANY COLUMN MASTER KEY DEFINITION* 資料庫權限，對話方塊才能建立資料行加密金鑰中繼資料以及存取資料行主要金鑰中繼資料。
若要存取金鑰存放區，並使用資料行主要金鑰，您可能需要金鑰存放區和/或金鑰的權限︰
- **憑證存放區 – 本機電腦** - 您必須具有當成資料行主要金鑰使用之憑證的讀取權，或為電腦上的系統管理員。
- **Azure 金鑰保存庫** - 您需要具有包含資料行主要金鑰之保存庫的 *get*、 *unwrapKey*、 *wrapKey*、 *sign*和 *verify*  權限。
- **金鑰存放區提供者 (CNG)** - 使用金鑰存放區或金鑰時，系統可能會提示您提供必要權限和認證 (取決於存放區和 KSP 組態)。
- **密碼編譯服務提供者 (CAPI)** - 使用金鑰存放區或金鑰時，系統可能會提示您提供必要權限和認證 (取決於存放區和 CSP 組態)。

如需詳細資訊，請參閱 [建立及儲存資料行主要金鑰 (永遠加密)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)。

<a name="rotatecmk"></a>
## <a name="rotating-column-master-keys"></a>輪替資料行主要金鑰

資料行主要金鑰輪替是一項以新資料行主要金鑰來取代現有資料行主要金鑰的程序。 如果金鑰已遭洩漏，或是為了符合您的組織原則或必須定期更換授權密碼編譯金鑰的標準規定，您可能必須更換金鑰。 資料行主要金鑰輪替包含解密目前資料行主要金鑰所保護的資料行加密金鑰、使用新的資料行主要金鑰重新進行加密，以及更新金鑰中繼資料。 如需詳細資訊，請參閱 [永遠加密的金鑰管理概觀](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)。

**步驟 1︰佈建新的資料行主要金鑰**

遵循上述＜佈建資料行主要金鑰＞一節中的步驟，佈建新資料行主要金鑰。

**步驟 2︰使用新的資料行主要金鑰來將資料行加密金鑰加密**

資料行主要金鑰通常會保護一或多個資料行加密金鑰。 每個資料行加密金鑰在資料庫中皆存有加密值，其為使用資料行主要金鑰將資料行加密金鑰加密的產物。
在此步驟中，使用新資料行主要金鑰，將輪替中資料行主要金鑰所保護的每個資料行加密金鑰加密，並將新加密值儲存在資料庫中。 因此，每個受到輪替影響的資料行加密金鑰皆會有兩個加密值︰其中一個值是由現有資料行主要金鑰加密，而另一個新值是由新資料行主要金鑰加密。

1.    使用物件總管****，巡覽至 [安全性] > [永遠加密金鑰] > [資料行主要金鑰]**** 資料夾，並找出輪替中資料行主要金鑰。
2.    以滑鼠右鍵按一下資料行主要金鑰，然後選取 [輪替]****。
3.    在 [資料行主要金鑰輪替] **** 對話方塊的 [目標] **** 欄位中，選取您在步驟 1 中建立之新資料行主要金鑰的名稱。
4.    檢閱現有資料行主要金鑰所保護的資料行加密金鑰清單。 這些金鑰將會受到輪替影響。
5.    按一下 **[確定]**。

SQL Server Management Studio 將會取得舊資料行主要金鑰所保護之資料行加密金鑰的中繼資料，以及舊與新資料行主要金鑰的中繼資料。 SSMS 接著將使用資料行主要金鑰中繼資料來存取包含舊資料行主要金鑰的金鑰存放區，並解密資料行加密金鑰。 接著，SSMS 將存取保存新資料行主要金鑰的金鑰存放區，以產生資料行加密金鑰的一組新加密值，接著將新值新增至中繼資料 (產生並發出 [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md) 陳述式)。

> [!NOTE]
> 請確定舊資料行主要金鑰所加密的每個資料行加密金鑰，皆不會由任何其他資料行主要金鑰所加密。 換句話說，每個受到替換影響的資料行加密金鑰，在資料庫中皆必須正好只有一個加密值。 如果任何受影響的資料行加密金鑰有一個以上的加密值，則您需要移除該值，才可以繼續使用輪替 (請參閱步驟 4 ** 了解如何移除資料行加密金鑰的加密值)。

**步驟 3︰使用新的資料行主要金鑰設定您的應用程式**

在此步驟中，您需要確定查詢輪替中資料行主要金鑰所保護的資料庫資料行 (也就是使用資料行加密金鑰加密的資料庫資料行，而該加密金鑰由輪替中資料行主要金鑰加密) 的所有用戶端應用程式，皆可以存取新資料行主要金鑰。 此步驟取決於新資料行主要金鑰所在金鑰存放區的類型。 例如：
- 若新資料行主要金鑰是儲存在 Windows 憑證存放區的憑證，則您需要將憑證部署至同一個憑證存放區位置 (「目前使用者」** 或「本機電腦」 **)，作為資料庫中資料行主要金鑰的金鑰路徑中所指定的位置。 應用程式必須能夠存取憑證︰
    - 如果憑證儲存在「目前使用者」 ** 憑證存放區位置中，憑證必須匯入應用程式的 Windows 身分識別 (使用者) 的「目前使用者」存放區。
    - 如果憑證儲存在「本機電腦」 ** 憑證存放區位置中，應用程式的 Windows 身分識別必須有權存取憑證。
- 若新資料行主要金鑰儲存在 Microsoft Azure 金鑰保存庫中，就必須實作應用程式，使其可以向 Azure 驗證並有權存取金鑰。

如需詳細資訊，請參閱 [建立和儲存資料行主要金鑰 (永遠加密)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)。

> [!NOTE]
> 在輪替的這個時間點，舊資料行主要金鑰和新資料行主要金鑰皆為有效，且可以用來存取資料。

**步驟 4︰清除舊資料行主要金鑰所加密的資料行加密金鑰值**

將所有應用程式設定為使用新資料行主要金鑰後，從資料庫移除舊 ** 資料行主要金鑰所加密的資料行加密金鑰值。 移除舊值可確保您準備好進行下一個輪替 (請記住，要輪替的資料行主要金鑰所保護的每個資料行加密金鑰皆必須正好只有一個加密值)。

另一個要在封存或移除舊資料行主要金鑰前清除舊值的原因與效能相關：在查詢加密資料行時，已啟用永遠加密的用戶端驅動程式可能需要嘗試解密兩個值︰舊值和新值。 驅動程式不知道在應用程式環境中，這兩個資料行主要金鑰中哪一個有效，因此驅動程式會從伺服器擷取這兩個加密值。 若其中一個值是受到已無法使用的資料行主要金鑰 (例如該舊資料行主要金鑰已從存放區移除) 保護而造成解密失敗，則驅動程式會嘗試使用新資料行主要金鑰來解密另一個值。

> [!WARNING]
> 若您先行移除資料行加密金鑰的值，而應用程式尚無法使用其對應的資料行主要金鑰，則該應用程式將無法再解密資料庫資料行。

1.    使用物件總管****，巡覽至 [安全性] > [永遠加密金鑰]**** 資料夾，並找出要取代的現有資料行主要金鑰。
2.    以滑鼠右鍵按一下現有資料行主要金鑰，然後選取 [清除]****。
3.    檢閱要移除的資料行加密金鑰值清單。
4.    按一下 **[確定]**。

SQL Server Management Studio 將會發出 [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md) 陳述式，來捨棄舊資料行主要金鑰所加密之資料行加密金鑰的加密值。

**步驟 5︰刪除舊資料行主要金鑰的中繼資料**

如果您選擇從資料庫移除舊資料行主要金鑰的定義，請使用下列步驟。 
1.    使用物件總管****，巡覽至 安全性 > 永遠加密金鑰} > 資料行主要金鑰**** 資料夾，然後找出要從資料庫移除的舊資料行主要金鑰。
2.    以滑鼠右鍵按一下舊資料行主要金鑰，然後選取 [刪除]****。 (這樣會產生並發出 [DROP COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md) 陳述式來移除資料行主要金鑰中繼資料)。
3.    按一下 **[確定]**。

> [!NOTE]
> 強烈建議您不要在輪替之後永久刪除舊資料行主要金鑰。 而是應該將舊資料行主要金鑰保留在其目前金鑰存放區中，或將它封存在另一個安全的地方。 如果您將資料庫從備份檔案還原到設定新資料行主要金鑰之前的某個時間點，則需要舊的金鑰才能存取資料。

### <a name="permissions"></a>Permissions

輪替資料行主要金鑰需要下列資料庫權限︰

- **ALTER ANY COLUMN MASTER KEY** - 建立新資料行主要金鑰的中繼資料以及刪除舊資料行主要金鑰之中繼資料時的必要項目。
- **ALTER ANY COLUMN ENCRYPTION KEY** - 修改資料行加密金鑰中繼資料 (新增加密值) 時的必要項目。
- **VIEW ANY COLUMN MASTER KEY DEFINITION** - 存取和讀取資料行主要金鑰中繼資料時的必要項目。
- **VIEW ANY COLUMN ENCRYPTION KEY DEFINITION** - 存取和讀取資料行加密金鑰中繼資料時的必要項目。 

您也需要可以在金鑰存放區中存取舊資料行主要金鑰和新資料行主要金鑰。 若要存取金鑰存放區，並使用資料行主要金鑰，您可能需要金鑰存放區和/或金鑰的權限︰
- **憑證存放區 – 本機電腦** - 您必須具有當成資料行主要金鑰使用之憑證的讀取權，或為電腦上的系統管理員。
- **Azure 金鑰保存庫** - 您需要具有包含資料行主要金鑰之保存庫的 *create*、 *get*、 *unwrapKey*、 *wrapKey*、 *sign*和 *verify* 權限。
- **金鑰存放區提供者 (CNG)** - 使用金鑰存放區或金鑰時，系統可能會提示您提供必要權限和認證 (取決於存放區和 KSP 組態)。
- **密碼編譯服務提供者 (CAPI)** - 使用金鑰存放區或金鑰時，系統可能會提示您提供必要權限和認證 (取決於存放區和 CSP 組態)。

如需詳細資訊，請參閱 [建立及儲存資料行主要金鑰 (永遠加密)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)。

<a name="rotatecek"></a> 
## <a name="rotating-column-encryption-keys"></a>輪替資料行加密金鑰

輪替資料行加密金鑰包括解密該金鑰所加密之所有資料行中要轉出的資料，以及使用新的資料行加密金鑰重新加密資料。

>[!NOTE]
> 如果包含輪替中金鑰所加密之資料行的資料表很大，則輪替資料行加密金鑰可能需要很長的時間。 正在重新加密資料時，您的應用程式無法寫入受影響的資料表中。 因此，您的組織需要非常仔細地規劃資料行加密金鑰輪替。
若要輪替資料行加密金鑰，請使用 [永遠加密精靈]。

1.    開啟資料庫的精靈：以滑鼠右鍵按一下資料庫，並指向 [工作] ****，然後按一下 [加密資料行] ****。
2.    檢閱[簡介] **** 頁面，然後按一下 [下一步] ****。
3.    在 [資料行選取] **** 頁面上，展開資料表，然後找出舊資料行加密金鑰目前所加密且您想要取代的所有資料行。
4.    對於舊資料行加密金鑰所加密的每個資料行，將 [加密金鑰] **** 設定為新的自動產生金鑰。 **注意：** 或者，您可以先建立新的資料行加密金鑰，再執行精靈 – 請參閱上述的＜佈建資料行加密金鑰＞ ** 一節。
5.    在 [主要金鑰組態] **** 頁面上，選取要儲存新金鑰的位置，並選取主要金鑰來源，然後按一下 [下一步] ****。 **注意：** 如果您使用的是現有資料行加密金鑰，而非自動產生的資料行加密金鑰，則不需要在這個頁面上執行任何動作。
6.    在 [驗證] ****頁面上，選擇是否要立即執行指令碼或建立 PowerShell 指令碼，然後按一下 [下一步] ****。
7.    在 [摘要] **** 頁面上，檢閱您已選取的選項，並按一下 [完成] **** ，然後在完成時關閉精靈。
8.    使用物件總管 ****，巡覽至 [安全性]/[永遠加密金鑰]/[資料行加密金鑰] **** 資料夾，然後找出要從資料庫移除的舊資料行加密金鑰。 以滑鼠右鍵按一下金鑰，然後選取 [刪除] ****。

### <a name="permissions"></a>Permissions

輪替資料行加密金鑰需要下列的資料庫權限︰ **ALTER ANY COLUMN MASTER KEY** - 如果您使用新的自動產生資料行加密金鑰 (也會產生新的資料行主要金鑰和其新的中繼資料)，則其為必要項目。
**ALTER ANY COLUMN ENCRYPTION KEY** - 新增新資料行加密金鑰之中繼資料時的必要項目。
**VIEW ANY COLUMN MASTER KEY DEFINITION** - 存取和讀取資料行主要金鑰中繼資料時的必要項目。
**VIEW ANY COLUMN ENCRYPTION KEY DEFINITION** - 存取和讀取資料行加密金鑰中繼資料時的必要項目。

您也需要可以存取新和舊資料行加密金鑰的資料行主要金鑰。 若要存取金鑰存放區，並使用資料行主要金鑰，您可能需要金鑰存放區和/或金鑰的權限︰
- **憑證存放區 – 本機電腦** - 您必須具有當成資料行主要金鑰使用之憑證的讀取權，或為電腦上的系統管理員。
- **Azure 金鑰保存庫** - 您需要具有包含資料行主要金鑰之保存庫的 get、unwrapKey 和 verify 權限。
- **金鑰存放區提供者 (CNG)** - 使用金鑰存放區或金鑰時，系統可能會提示您提供必要權限和認證 (取決於存放區和 KSP 組態)。
- **密碼編譯服務提供者 (CAPI)** - 使用金鑰存放區或金鑰時，系統可能會提示您提供必要權限和認證 (取決於存放區和 CSP 組態)。

如需詳細資訊，請參閱 [建立及儲存資料行主要金鑰 (永遠加密)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)。

## <a name="performing-dac-upgrade-operations-when-database-or-dacpac-uses-always-encrypted"></a>當資料庫或 DACPAC 使用永遠加密時，執行 DAC 升級作業

在具有包含加密資料行之結構描述的 DACPAC 檔案和資料庫上，支援[DAC 作業](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_3) 。 特殊考量適用於 DAC 升級作業 - 請參閱 [升級資料層應用程式](../../../relational-databases/data-tier-applications/upgrade-a-data-tier-application.md) 的有關如何使用各種工具 (包含 SSMS) 執行 DAC 升級作業。 

如果您使用 DACPAC 升級資料庫，而且 DACPAC 或目標資料庫包含加密資料行，則升級作業會在符合下列所有條件時觸發資料加密作業︰
- 資料庫包含具有資料的資料行。
- 相同的資料行存在於 DACPAC 中。
- 資料庫中資料行的加密組態與 DACPAC 中對應資料行的組態不同。 如需詳細資訊，請參閱下表。

| 條件|動作|
|:---|:---|
|資料行已在 DACPAC 中進行加密，但未在資料庫中進行加密。| 將會加密資料行中的資料。|
|資料行未在 DACPAC 中進行加密，但會在資料庫中進行加密。| 將會解密資料行中的資料 (將會移除資料行的加密)。|
| 資料行已在 DACPAC 和資料庫中進行加密，但是 DACPAC 中的資料行會使用與資料庫中對應資料行不同的加密類型和/或不同的資料行加密金鑰。|將會解密資料行中的資料，然後重新加密以符合 DACPAC 中的加密組態。|

> [!NOTE]
> 如果針對資料庫或 DACPAC 中資料行所設定的資料行主要金鑰儲存在 Azure 金鑰保存庫中，則系統會提示您登入 Azure (如果尚未登入)。

### <a name="permissions"></a>Permissions

若要在 DACPAC 或目標資料庫中設定永遠加密時執行 DAC 升級作業，您可能需要具有下列部分或所有權限 (取決於 DACPAC 中的結構描述與目標資料庫結構描述之間的差異)。

*ALTER ANY COLUMN MASTER KEY*、 *ALTER ANY COLUMN ENCRYPTION KEY*、 *VIEW ANY COLUMN MASTER KEY DEFINITION*、 *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION*

如果升級作業觸發資料加密作業，則您也需要可以存取針對受影響資料行所設定的資料行主要金鑰︰
- **憑證存放區 – 本機電腦** - 您必須具有當成資料行主要金鑰使用之憑證的讀取權，或為電腦上的系統管理員。
- **Azure 金鑰保存庫** - 您需要具有包含資料行主要金鑰之保存庫的 *create*、 *get*、 *unwrapKey*、 *wrapKey*、 *sign*和 *verify* 權限。
- **金鑰存放區提供者 (CNG)** - 使用金鑰存放區或金鑰時，系統可能會提示您提供必要權限和認證 (取決於存放區和 KSP 組態)。
- **密碼編譯服務提供者 (CAPI)** - 使用金鑰存放區或金鑰時，系統可能會提示您提供必要權限和認證 (取決於存放區和 CSP 組態)。

如需詳細資訊，請參閱 [建立及儲存資料行主要金鑰 (永遠加密)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)。

## <a name="migrating-databases-with-encrypted-columns-using-bacpac"></a>使用 BACPAC 移轉具有加密資料行的資料庫

當您匯出資料庫時，加密資料行中所儲存的所有資料都會擷取並放入產生的 [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) (加密形式)。 產生的 BACPAC 也會包含永遠加密金鑰的中繼資料。

當您將 BACPAC 匯入資料庫中時，會將 BACPAC 中的加密資料載入資料庫中，並且重新建立永遠加密金鑰中繼資料。

如果您的應用程式設定成修改或擷取來源資料庫 (您匯出的資料庫) 中所儲存的加密資料，則不需要執行任何特殊作業，就可讓應用程式查詢目標資料庫中的加密資料，因為兩個資料庫中的金鑰都相同。


### <a name="permissions"></a>Permissions

您需要具有來源資料庫的 *ALTER ANY COLUMN MASTER KEY* 和 *ALTER ANY COLUMN ENCRYPTION KEY* 。 您需要具有目標資料庫的 *ALTER ANY COLUMN MASTER KEY*、 *ALTER ANY COLUMN ENCRYPTION KEY*、 *VIEW ANY COLUMN MASTER KEY DEFINITION*和 *VIEW ANY COLUMN ENCRYPTION* 。

## <a name="migrating-databases-with-encrypted-columns-using-sql-server-import-and-export-wizard"></a>使用 SQL Server 匯入和匯出精靈移轉具有加密資料行的資料庫

相較於使用 BACPAC 檔案， [SQL Server 匯入和匯出精靈](~/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md) 可讓您深入控制如何在資料移轉期間處理加密資料行中所儲存的資料。

- 如果您的資料來源是使用永遠加密的資料庫，則可以設定資料來源連接，以在匯出作業期間解密加密資料行中所儲存的資料，或維持加密狀態。
- 如果您的資料目標是使用永遠加密的資料庫，則可以設定資料目標連接，以加密目標設為加密資料行的資料。

若要啟用解密 (針對資料來源) 或加密 (針對資料目標)，您需要將資料來源/目標連接設定成使用 [.Net Framework Data Provider for SqlServer](https://msdn.microsoft.com/library/system.data.sqlclient.aspx) ，而且需要將資料行加密設定連接字串關鍵字設成 [已啟用] **。

下表列出可能的移轉案例、它們與永遠加密的關係，以及每個連接的資料來源和資料目標組態。

| 狀況|來源連接組態|    目標連接組態
|:---|:---|:---
|在移轉時加密資料 (資料會以純文字形式儲存在資料來源中，並移轉至資料目標的加密資料行中)。| 資料提供者/驅動程式︰任何 **<br><br>資料行加密設定 = 已停用<br><br>(如果使用 SqlServer 和 .NET Framework 4.6 或更新版本的 .Net Framework 資料提供者。) | 資料提供者/驅動程式︰ *SqlServer 的 .Net Framework 資料提供者* (需要 .NET Framework 4.6 或更新版本)<br><br>資料行加密設定 = 已啟用
| 在移轉時解密資料 (資料會儲存在資料來源的加密資料行中，並且以純文字形式移轉至資料目標；如果資料目標是資料庫，則不會加密目標資料行)。<br><br>**注意：** 移轉之前，必須要有具有加密資料行的目標資料表。|資料提供者/驅動程式︰ *SqlServer 的 .Net Framework 資料提供者* (需要 .NET Framework 4.6 或更新版本)<br><br>資料行加密設定 = 已啟用|資料提供者/驅動程式︰任何 **<br><br>資料行加密設定 = 已停用<br><br>(如果使用 SqlServer 和 .NET Framework 4.6 或更新版本的 .Net Framework 資料提供者。)
|在移轉時重新加密資料 (資料會儲存在資料來源的加密資料行中，並且以純文字形式移轉至資料目標中使用不同加密類型之資料行加密金鑰的資料行)。<br><br>**注意：** 移轉之前，必須要有具有加密資料行的目標資料表。| 資料提供者/驅動程式︰ *SqlServer 的 .Net Framework 資料提供者* (需要 .NET Framework 4.6 或更新版本)<br><br>資料行加密設定 = 已啟用|資料提供者/驅動程式︰ *SqlServer 的 .Net Framework 資料提供者* (需要 .NET Framework 4.6 或更新版本)<br><br>資料行加密設定 = 已啟用
|移動加密資料，而未進行解密。<br><br>**注意：** 移轉之前，必須要有具有加密資料行的目標資料表。| 資料提供者/驅動程式︰任何 **<br>資料行加密設定 = 已停用<br><br>(如果使用 SqlServer 和 .NET Framework 4.6 或更新版本的 .Net Framework 資料提供者。)| 資料提供者/驅動程式︰任何 **<br>資料行加密設定 = 已停用<br><br>(如果使用 SqlServer 和 .NET Framework 4.6 或更新版本的 .Net Framework 資料提供者。)<br><br>使用者必須將 ALLOW_ENCRYPTED_VALUE_MODIFICATIONS 設成 ON。<br><br>如需詳細資訊，請參閱 [移轉透過永遠加密保護的敏感性資料](../../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md)。


### <a name="permissions"></a>Permissions

若要 **加密** 或 **解密** 資料來源中所儲存的資料，您需要具有來源資料庫的 *VIEW ANY COLUMN MASTER KEY DEFINITION* 和 *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* 權限。

您也需要存取針對資料行所設定的資料行主要金鑰，而資料行主要金鑰用來儲存所加密或解密的資料：
- **憑證存放區 – 本機電腦** - 您必須具有當成資料行主要金鑰使用之憑證的讀取權，或為電腦上的系統管理員。
- **Azure 金鑰保存庫** - 您需要具有包含資料行主要金鑰之保存庫的 get、unwrapKey、wrapKey、sign 和 verify 權限。
- **金鑰存放區提供者 (CNG)** - 必要權限和認證 (您在使用金鑰存放區或金鑰時可能收到提示) 取決於存放區和 KSP 組態。
- **密碼編譯服務提供者 (CAPI)** - 必要權限和認證 (您在使用金鑰存放區或金鑰時可能會收到提示) 取決於存放區和 CSP 組態。
如需詳細資訊，請參閱 [建立及儲存資料行主要金鑰 (永遠加密)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)。

## <a name="see-also"></a>另請參閱
- [Always Encrypted (資料庫引擎)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted 精靈](../../../relational-databases/security/encryption/always-encrypted-wizard.md)
- [Always Encrypted 的金鑰管理概觀](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [建立及儲存資料行主要金鑰 (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)
- [Always Encrypted (用戶端開發)](../../../relational-databases/security/encryption/always-encrypted-client-development.md)
- [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)
- [DROP COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md)
- [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md)
- [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md)
- [DROP COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/drop-column-encryption-key-transact-sql.md) 
- [sys.column_master_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
- [sys.column_encryption_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)
- [使用 PowerShell 設定 Always Encrypted](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)













