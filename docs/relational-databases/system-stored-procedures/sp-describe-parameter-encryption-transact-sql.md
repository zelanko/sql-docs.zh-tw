---
title: sp_describe_parameter_encryption （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 07/27/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
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
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c4a4cfe5c86d39766bcd322b879172b00b33eb68
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "73593707"
---
# <a name="sp_describe_parameter_encryption-transact-sql"></a>sp_describe_parameter_encryption （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  分析指定[!INCLUDE[tsql](../../includes/tsql-md.md)]的語句和其參數，以判斷哪些參數對應至使用 Always Encrypted 功能保護的資料庫資料行。 針對對應至加密資料行的參數傳回加密中繼資料。  
  
## <a name="syntax"></a>語法  
  
```  
sp_describe_parameter_encryption   
    [ @tsql = ] N'Transact-SQL_batch' ,   
    [ @params = ] N'parameters'   
[ ;]  
```  
  
## <a name="arguments"></a>引數  
 [ \@tsql =]' SQL_batch transact-sql '  
 一個或多個 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 交易 SQL_batch 可以是 Nvarchar （n）或 Nvarchar （max）。  
  
 [ \@params =]N'parameters'  
 params 提供 transact-sql 批次參數的宣告字串，類似于 sp_executesql。 * \@ * 參數可以是 Nvarchar （n）或 Nvarchar （max）。  
  
 這是一個字串，其中包含已內嵌在[!INCLUDE[tsql](../../includes/tsql-md.md)]_batch 中之所有參數的定義。 此字串必須是 Unicode 常數或 Unicode 變數。 每個參數定義都由參數名稱和資料類型組成。 *n*是指出其他參數定義的預留位置。 語句中指定的每個參數都必須在* \@params*中定義。 如果語句[!INCLUDE[tsql](../../includes/tsql-md.md)]中的語句或批次不包含參數， * \@* 則不需要 params。 這個參數的預設值是 NULL。  
  
## <a name="return-value"></a>傳回值  
 0表示成功。 任何其他表示失敗的專案。  
  
## <a name="result-sets"></a>結果集  
 **sp_describe_parameter_encryption**會傳回兩個結果集：  
  
-   描述針對資料庫資料行所設定之密碼編譯金鑰的結果集，指定[!INCLUDE[tsql](../../includes/tsql-md.md)]之語句的參數會對應至。  
  
-   描述如何加密特定參數的結果集。 此結果集會參考第一個結果集中所述的索引鍵。  
  
 第一個結果集的每個資料列都會描述一對索引鍵;加密資料行加密金鑰及其對應的資料行主要金鑰。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**column_encryption_key_ordinal**|**int**|結果集中的資料列識別碼。|  
|**database_id**|**int**|資料庫識別碼。|  
|**column_encryption_key_id**|**int**|資料行加密金鑰識別碼。注意：此識別碼代表 sys.databases 中的資料列[column_encryption_keys &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)目錄檢視。|  
|**column_encryption_key_version**|**int**|保留供未來使用。 目前，一律包含1。|  
|**column_encryption_key_metadata_version**|**binary （8）**|表示資料行加密金鑰之建立時間的時間戳記。|  
|**column_encryption_key_encrypted_value**|**varbinary(4000)**|資料行加密金鑰的加密值。|  
|**column_master_key_store_provider_name**|**sysname**|包含資料行主要金鑰之金鑰存放區的提供者名稱，這是用來產生資料行加密金鑰的加密值。|  
|**column_master_key_path**|**nvarchar(4000)**|資料行主要金鑰的索引鍵路徑，用來產生資料行加密金鑰的加密值。|  
|**column_encryption_key_encryption_algorithm_name**|**sysname**|用來產生資料行加密金鑰之加密值的加密演算法名稱。|  
  
 第二個結果集的每一列都包含一個參數的加密中繼資料。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**parameter_ordinal**|**int**|結果集中資料列的識別碼。|  
|**parameter_name**|**sysname**|Params 引數中指定的其中一個參數名稱。 * \@ *|  
|**column_encryption_algorithm**|**tinyint**|表示為數據行設定之加密演算法的程式碼，參數會對應至。 目前支援的值為：2，適用于**AEAD_AES_256_CBC_HMAC_SHA_256**。|  
|**column_encryption_type**|**tinyint**|表示為數據行設定之加密類型的程式碼，參數會對應至。 支援的值為：<br /><br /> 0-純文字（資料行未加密）<br /><br /> 1-隨機加密<br /><br /> 2-具決定性的加密。|  
|**column_encryption_key_ordinal**|**int**|第一個結果集中的資料列程式碼。 參考的資料列描述針對資料行所設定的資料行加密金鑰，參數會對應至。|  
|**column_encryption_normalization_rule_version**|**tinyint**|類型正規化演算法的版本號碼。|  
  
## <a name="remarks"></a>備註  
 支援[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Always Encrypted 的用戶端驅動程式會自動呼叫**sp_describe_parameter_encryption** ，以取得應用程式所發出之參數化查詢的加密中繼資料。 接著，驅動程式會使用加密中繼資料來加密對應至以 Always Encrypted 保護之資料庫資料行的參數值，並以加密參數值取代應用程式所提交的純文字參數值，然後再將查詢傳送至資料庫引擎。  
  
## <a name="permissions"></a>權限  
 需要資料庫中的**VIEW ANY COLUMN ENCRYPTION KEY definition**和**VIEW ANY COLUMN MASTER KEY definition**許可權。  
  
## <a name="examples"></a>範例  
  
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
  
 （結果會繼續）。  
  
|column_master_key_store_provider_name|column_master_key_path|column_encryption_key_encryption_algorithm_name|  
|------------------------------------------------|-------------------------------|----------------------------------------------------------|  
|MSSQL_CERTIFICATE_STORE|CurrentUser/my/A66BB0F6DD70BDFF02B62D0F87E340288E6F9305|RSA_OAEP|  
  
 以下是第二個結果集：  
  
|parameter_ordinal|parameter_name|column_encryption_algorithm|column_encryption_type|  
|------------------------|---------------------|-----------------------------------|------------------------------|  
|1|\@c1|1|1|  
  
 （結果會繼續）。  
  
|column_encryption_key_ordinal|column_encryption_normalization_rule_version|  
|--------------------------------------|------------------------------------------------------|  
|1|1|  
  
## <a name="see-also"></a>另請參閱  
 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [使用 Always Encrypted 開發應用程式](../../relational-databases/security/encryption/always-encrypted-client-development.md)  
  
  
