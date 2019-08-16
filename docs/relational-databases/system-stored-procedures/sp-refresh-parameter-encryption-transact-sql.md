---
title: sp_refresh_parameter_encryption (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sp_refresh_parameter_encryption
- sp_refresh_parameter_encryption_TSQL
- sys.sp_refresh_parameter_encryption
- sys.sp_refresh_parameter_encryption_TSQL
helpviewer_keywords:
- sp_refresh_parameter_encryption
- Always Encrypted, sp_refresh_parameter_encryption
ms.assetid: 00b44baf-fcf0-4095-aabe-49fa87e77316
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a5f699f21b1f28537da2e2f0033fe6b17908186a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002458"
---
# <a name="sp_refresh_parameter_encryption-transact-sql"></a>sp_refresh_parameter_encryption & Amp;&#40;transact-SQL&AMP;&#41;
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

更新指定的非結構描述繫結預存程序、 使用者定義函數、 檢視、 DML 觸發程序、 資料庫層級 DDL 觸發程序，或目前資料庫中的伺服器層級 DDL 觸發程序參數的 Always Encrypted 中繼資料。 

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
sys.sp_refresh_parameter_encryption [ @name = ] 'module_name' 
    [ , [ @namespace = ] '<class>' ]
[ ; ]

<class> ::=
{ DATABASE_DDL_TRIGGER | SERVER_DDL_TRIGGER }
```

## <a name="arguments"></a>引數

`[ @name = ] 'module_name'` 是預存程序、 使用者定義函數、 檢視、 DML 觸發程序、 資料庫層級 DDL 觸發程序或伺服器層級 DDL 觸發程序的名稱。 *module_name*不能是 common language runtime (CLR) 預存程序或 CLR 函式。 *module_name*不可進行結構描述繫結。 *module_name*是`nvarchar`，沒有預設值。 *module_name*可以是多重部分識別碼，但只能參考目前資料庫中的物件。

`[ @namespace = ] ' < class > '` 為指定的模組類別。 當*module_name* DDL 觸發程序，`<class>`需要。 `<class>` 為 `nvarchar(20)`。 有效輸入如下`DATABASE_DDL_TRIGGER`和`SERVER_DDL_TRIGGER`。    

## <a name="return-code-values"></a>傳回碼值  

0 (成功) 或非零數字 (失敗)


## <a name="remarks"></a>備註

如果也可能會過期，加密中繼資料模組的參數：   
* [加密] 屬性已更新模組參考的資料表中的資料行。 比方說，已經卸除資料行，並已新增新的資料行，與相同的名稱，但不同的加密類型、 加密金鑰或加密演算法。  
* 模組參考另一個模組使用過期的參數加密中繼資料。  

修改資料表的加密屬性，當`sp_refresh_parameter_encryption`應該執行的任何直接或間接參考資料表的模組。 這個預存程序可以呼叫這些模組，依任何順序，而不需要再移至其呼叫端的使用者第一次重新整理的內部模組。

`sp_refresh_parameter_encryption` 不會影響任何權限，擴充屬性，或`SET`與物件相關聯的選項。 

若要重新整理伺服器層級 DDL 觸發程序，請從任何資料庫的內容執行此預存程序。

> [!NOTE]
>  當您執行時，會卸除與物件相關聯的任何簽章`sp_refresh_parameter_encryption`。

## <a name="permissions"></a>Permissions

需要`ALTER`在模組上的權限和`REFERENCES`任何 CLR 使用者定義型別和 XML 結構描述集合所參考的物件權限。   

當指定的模組是資料庫層級 DDL 觸發程序時，需要`ALTER ANY DATABASE DDL TRIGGER`目前資料庫中的權限。    

伺服器層級 DDL 觸發程序指定的模組時，需要`CONTROL SERVER`權限。

針對模組，以定義`EXECUTE AS`子句，`IMPERSONATE`指定的主體需要權限。 一般而言，重新整理物件不會變更其`EXECUTE AS`主體，除非模組以定義`EXECUTE AS USER`和主體現在解析成不同的使用者來得當時模組所建立的使用者名稱。
 
## <a name="examples"></a>範例

下列範例會建立資料表和參考資料表的程序、 設定永遠加密，並再示範改變資料表，以及執行`sp_refresh_parameter_encryption`程序。  

先建立初始的資料表和參考資料表的預存程序。
```sql
CREATE TABLE [Patients]([PatientID] [int] IDENTITY(1,1) NOT NULL,
    [SSN] [char](11), 
    [FirstName] [nvarchar](50) NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [MiddleName] [nvarchar](50) NULL,
    [StreetAddress] [nvarchar](50) NOT NULL,
    [City] [nvarchar](50) NOT NULL,
    [ZipCode] [char](5) NOT NULL,
    [State] [char](2) NOT NULL,
    [BirthDate] [date] NOT NULL,
 CONSTRAINT [PK_Patients] PRIMARY KEY CLUSTERED 
(
    [PatientID] ASC
) WITH 
    (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, 
     IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, 
     ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY];
GO

CREATE PROCEDURE [find_patient] @SSN [char](11)
AS
BEGIN
    SELECT * FROM [Patients] WHERE SSN=@SSN
END;
GO
```

然後設定永遠加密金鑰。
```sql
CREATE COLUMN MASTER KEY [CMK1]
WITH
(
       KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',
    KEY_PATH = N'CurrentUser/my/A66BB0F6DD70BDFF02B62D0F87E340288E6F9305'
);
GO

CREATE COLUMN ENCRYPTION KEY [CEK1]
WITH VALUES
(
       COLUMN_MASTER_KEY = [CMK1],
    ALGORITHM = 'RSA_OAEP',
    ENCRYPTED_VALUE = 
       0x016E000001630075007200720065006E00740075007300650072002F006D0079002F006100360036006200620030006600360064006400370030006200640066006600300032006200360032006400300066003800370065003300340030003200380038006500360066003900330030003500CA0D0CEC74ECADD1804CF99137B4BD06BBAB15D7EA74E0C249A779C7768A5B659E0125D24FF827F5EA8CA517A8E197ECA1353BA814C2B0B2E6C8AB36E3AE6A1E972D69C3C573A963ADAB6686CF5D24F95FE43140C4F9AF48FBA7DF2D053F3B4A1F5693A1F905440F8015BDB43AF8A04BE4E045B89876A0097E5FBC4E6A3B9C3C0D278C540E46C53938B8C957B689C4DC095821C465C73117CBA95B758232F9E5B2FCC7950B8CA00AFE374DE42847E3FBC2FDD277035A2DEF529F4B735C20D980073B4965B4542A34723276A1646998FC6E1C40A3FDB6ABCA98EE2B447F114D2AC7FF8C7D51657550EC5C2BABFFE8429B851272086DCED94332CF18FA854C1D545A28B1EF4BE64F8E035175C1650F6FC5C4702ACF99850A4542B3747EAEC0CC726E091B36CE24392D801ECAA684DE344FECE05812D12CD72254A014D42D0EABDA41C89FC4F545E88B4B8781E5FAF40D7199D4842D2BFE904D209728ED4F527CBC169E2904F6E711FF81A8F4C25382A2E778DD2A58552ED031AFFDA9D9D891D98AD82155F93C58202FC24A77F415D4F8EF22419D62E188AC609330CCBD97CEE1AEF8A18B01958833604707FDF03B2B386487CC679D7E352D0B69F9FB002E51BCD814D077E82A09C14E9892C1F8E0C559CFD5FA841CEF647DAB03C8191DC46B772E94D579D8C80FE93C3827C9F0AE04D5325BC73111E07EEEDBE67F1E2A73580085
);
GO
```


最後，我們將取代 SSN 資料行加密的資料行，然後再執行`sp_refresh_parameter_encryption`程序來更新 Always Encrypted 的元件。
```sql
ALTER TABLE [Patients] DROP COLUMN [SSN];
GO

ALTER TABLE [Patients] 
    ADD [SSN] [char](11) COLLATE Latin1_General_BIN2 
    ENCRYPTED WITH 
        (COLUMN_ENCRYPTION_KEY = [CEK1], 
        ENCRYPTION_TYPE = Deterministic, 
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') 
    NOT NULL;
GO

EXEC sp_refresh_parameter_encryption [find_patient];
GO
```

## <a name="see-also"></a>另請參閱 

[Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
[Always Encrypted 精靈](../../relational-databases/security/encryption/always-encrypted-wizard.md)   

