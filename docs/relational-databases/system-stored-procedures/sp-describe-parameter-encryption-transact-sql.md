---
title: sp_describe_parameter_encryption (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 07/27/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_describe_parameter_encryption
- sp_describe_parameter_encryption_TSQL
- sys.sp_describe_parameter_encryption
- sys.sp_describe_parameter_encryption_TSQL
helpviewer_keywords:
- sp_describe_parameter_encryption
ms.assetid: 706ed441-2881-4934-8d5e-fb357ee067ce
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 377a1e342970e9593b37924c3739ee7a706d5264
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053030"
---
# <a name="spdescribeparameterencryption-transact-sql"></a>sp_describe_parameter_encryption & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  分析指定[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式和其參數，以判斷哪一個參數會對應至使用 Always Encrypted 功能保護的資料庫資料行。 傳回對應至加密的資料行的參數加密中繼資料。  
  
## <a name="syntax"></a>語法  
  
```  
sp_describe_parameter_encryption   
    [ @tsql = ] N'Transact-SQL_batch' ,   
    [ @params = ] N'parameters'   
[ ;]  
```  
  
## <a name="arguments"></a>引數  
 [ \@tsql =] ' Transact SQL_batch'  
 一個或多個 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 Transact SQL_batch 可能是 nvarchar （n） 或 nvarchar （max）。  
  
 [ \@params =] N'parameters'  
 *\@params*提供 TRANSACT-SQL 批次，類似於 sp_executesql 的參數宣告字串。 參數可能是 nvarchar （n） 或 nvarchar （max）。  
  
 是一個字串，其中包含之所有參數的已內嵌在定義[!INCLUDE[tsql](../../includes/tsql-md.md)]_batch&lt。 此字串必須是 Unicode 常數或 Unicode 變數。 每個參數定義都由參數名稱和資料類型組成。 *n*是指出其他參數定義的預留位置。 陳述式中指定的每個參數必須定義在 *\@params*。 如果[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式或陳述式中的批次不包含參數，  *\@params*並非必要。 這個參數的預設值是 NULL。  
  
## <a name="return-value"></a>傳回值  
 0 表示成功。 任何其他項目表示失敗。  
  
## <a name="result-sets"></a>結果集  
 **sp_describe_parameter_encryption**傳回兩個結果集：  
  
-   在結果集描述針對資料庫資料行，指定的參數設定的密碼編譯金鑰[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式對應至。  
  
-   結果集描述如何特定參數應該加密。 此結果集第一個結果集所述的索引鍵的參考。  
  
 第一個結果集的每個資料列描述一組金鑰;加密資料行加密金鑰和其對應的資料行主要金鑰。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**column_encryption_key_ordinal**|**int**|在結果集資料列的識別碼。|  
|**database_id**|**int**|資料庫識別碼。|  
|**column_encryption_key_id**|**int**|資料行加密金鑰識別碼。注意： 這個 id 表示中的資料列[sys.column_encryption_keys &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)目錄檢視。|  
|**column_encryption_key_version**|**int**|保留供日後使用。 目前，一定會包含 1。|  
|**column_encryption_key_metadata_version**|**binary(8)**|時間戳記，表示資料行加密金鑰的建立時間。|  
|**column_encryption_key_encrypted_value**|**varbinary(4000)**|資料行加密金鑰加密的值。|  
|**column_master_key_store_provider_name**|**sysname**|包含用來產生資料行加密金鑰的加密的值的資料行主要金鑰的金鑰存放區提供者名稱。|  
|**column_master_key_path**|**nvarchar(4000)**|資料行主要金鑰，用來產生資料行加密金鑰的加密的值的機碼的路徑。|  
|**column_encryption_key_encryption_algorithm_name**|**sysname**|用來產生資料行加密金鑰的加密值的加密演算法名稱。|  
  
 第二個結果集的每個資料列會包含一個參數的加密中繼資料。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**parameter_ordinal**|**int**|在結果集中的資料列的識別碼。|  
|**parameter_name**|**sysname**|其中一個指定的參數名稱 *\@params*引數。|  
|**column_encryption_algorithm**|**tinyint**|指出資料行，此參數設定的加密演算法的程式碼會對應至。 目前支援的值為：2 **AEAD_AES_256_CBC_HMAC_SHA_256**。|  
|**column_encryption_type**|**tinyint**|指出資料行，此參數設定的加密類型的程式碼會對應至。 支援的值為：<br /><br /> 0-純文字 （未加密的資料行）<br /><br /> 1-隨機化加密進行加密<br /><br /> 2-決定性加密。|  
|**column_encryption_key_ordinal**|**int**|程式碼中的第一個結果的資料列的設定。 參考的資料列描述資料行設定資料行加密金鑰，將參數對應至。|  
|**column_encryption_normalization_rule_version**|**tinyint**|型別正規化演算法的版本號碼。|  
  
## <a name="remarks"></a>備註  
 A[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端驅動程式，支援 Always Encrypted，會自動呼叫**sp_describe_parameter_encryption**來擷取應用程式所發出的參數化查詢的加密中繼資料。 接下來，驅動程式用以加密的參數對應到以 Always Encrypted 保護的資料庫資料行值的加密中繼資料，並會取代送出的應用程式，以將加密的純文字參數值參數值，再將查詢傳送至 database engine。  
  
## <a name="permissions"></a>Permissions  
 需要**VIEW ANY COLUMN ENCRYPTION KEY DEFINITION**並**VIEW ANY COLUMN MASTER KEY DEFINITION**資料庫中的權限。  
  
## <a name="examples"></a>範例  
  
```  
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
0x016E000001630075007200720065006E00740075007300650072002F006D007  
9002F00610036003600620062003000660036006400640037003000620064006  
6006600300032006200360032006400300066003800370065003300340030003  
200380038006500360066003900330030003500CA0D0CEC74ECADD1804CF991  
37B4BD06BBAB15D7EA74E0C249A779C7768A5B659E0125D24FF827F5EA8CA51  
7A8E197ECA1353BA814C2B0B2E6C8AB36E3AE6A1E972D69C3C573A963ADAB6  
686CF5D24F95FE43140C4F9AF48FBA7DF2D053F3B4A1F5693A1F905440F8015B  
DB43AF8A04BE4E045B89876A0097E5FBC4E6A3B9C3C0D278C540E46C53938B8  
C957B689C4DC095821C465C73117CBA95B758232F9E5B2FCC7950B8CA00AFE3  
74DE42847E3FBC2FDD277035A2DEF529F4B735C20D980073B4965B4542A3472  
3276A1646998FC6E1C40A3FDB6ABCA98EE2B447F114D2AC7FF8C7D51657550E  
C5C2BABFFE8429B851272086DCED94332CF18FA854C1D545A28B1EF4BE64F8E0  
35175C1650F6FC5C4702ACF99850A4542B3747EAEC0CC726E091B36CE24392D8  
01ECAA684DE344FECE05812D12CD72254A014D42D0EABDA41C89FC4F545E88B  
4B8781E5FAF40D7199D4842D2BFE904D209728ED4F527CBC169E2904F6E711FF8  
1A8F4C25382A2E778DD2A58552ED031AFFDA9D9D891D98AD82155F93C58202F  
C24A77F415D4F8EF22419D62E188AC609330CCBD97CEE1AEF8A18B0195883360  
4707FDF03B2B386487CC679D7E352D0B69F9FB002E51BCD814D077E82A09C14E  
9892C1F8E0C559CFD5FA841CEF647DAB03C8191DC46B772E94D579D8C80FE93C  
3827C9F0AE04D5325BC73111E07EEEDBE67F1E2A73580085  
);  
GO  
  
CREATE TABLE t1 (  
c1 INT ENCRYPTED WITH (  
    COLUMN_ENCRYPTION_KEY = [CEK_Auto1],   
    ENCRYPTION_TYPE = Randomized,   
    ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NULL,  
);  
  
EXEC sp_describe_parameter_encryption N'INSERT INTO t1 VALUES(@c1)',  N'@c1 INT';  
```  
  
 以下是第一個結果集：  
  
|column_encryption_key_ordinal|database_id|column_encryption_key_id|column_encryption_key_version|column_encryption_key_metadata_version|column_encryption_key_encrypted_value|  
|--------------------------------------|------------------|---------------------------------|--------------------------------------|------------------------------------------------|-----------------------------------------------|  
|1|5|1|1|0x99EDA60083A50000|0x016E000001630075007200720065006E00740075007300650072002F006D0079002F006100360036006200620030006600360064006400370030006200640066006600300032006200360032006400300066003800370065003300340030003200380038006500360066003900330030003500CA0D0CEC74ECADD1804CF99137B4BD06BBAB15D7EA74E0C249A779C7768A5B659E0125D24FF827F5EA8CA517A8E197ECA1353BA814C2B0B2E6C8AB36E3AE6A1E972D69C3C573A963ADAB6686CF5D24F95FE43140C4F9AF48FBA7DF2D053F3B4A1F5693A1F905440F8015BDB43AF8A04BE4E045B89876A0097E5FBC4E6A3B9C3C0D278C540E46C53938B8C957B689C4DC095821C465C73117CBA95B758232F9E5B2FCC7950B8CA00AFE374DE42847E3FBC2FDD277035A2DEF529F4B735C20D980073B4965B4542A34723276A1646998FC6E1C40A3FDB6ABCA98EE2B447F114D2AC7FF8C7D51657550EC5C2BABFFE8429B851272086DCED94332CF18FA854C1D545A28B1EF4BE64F8E035175C1650F6FC5C4702ACF99850A4542B3747EAEC0CC726E091B36CE24392D801ECAA684DE344FECE05812D12CD72254A014D42D0EABDA41C89FC4F545E88B4B8781E5FAF40D7199D4842D2BFE904D209728ED4F527CBC169E2904F6E711FF81A8F4C25382A2E778DD2A58552ED031AFFDA9D9D891D98AD82155F93C58202FC24A77F415D4F8EF22419D62E188AC609330CCBD97CEE1AEF8A18B01958833604707FDF03B2B386487CC679D7E352D0B69F9FB002E51BCD814D077E82A09C14E9892C1F8E0C559CFD5FA841CEF647DAB03C8191DC46B772E94D579D8C80FE93C3827C9F0AE04D5325BC73111E07EEEDBE67F1E2A73580085|  
  
 （結果繼續）。  
  
|column_master_key_store_provider_name|column_master_key_path|column_encryption_key_encryption_algorithm_name|  
|------------------------------------------------|-------------------------------|----------------------------------------------------------|  
|MSSQL_CERTIFICATE_STORE|CurrentUser/my/A66BB0F6DD70BDFF02B62D0F87E340288E6F9305|RSA_OAEP|  
  
 第二個結果集如下：  
  
|parameter_ordinal|parameter_name|column_encryption_algorithm|column_encryption_type|  
|------------------------|---------------------|-----------------------------------|------------------------------|  
|1|\@c1|1|1|  
  
 （結果繼續）。  
  
|column_encryption_key_ordinal|column_encryption_normalization_rule_version|  
|--------------------------------------|------------------------------------------------------|  
|1|1|  
  
## <a name="see-also"></a>另請參閱  
 [永遠加密 &#40;Database Engine&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [永遠加密 &#40;用戶端開發&#41;](../../relational-databases/security/encryption/always-encrypted-client-development.md)  
  
  
