---
title: SqlPackage.exe |Microsoft 文件
ms.custom:
- SSDT
ms.date: 2017-04-26
ms.prod: sql-non-specified
ms.reviewer: alayu; sstein
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 198198e2-7cf4-4a21-bda4-51b36cb4284b
caps.latest.revision: 53
author: pensivebrian
ms.author: broneill
manager: craigg
ms.openlocfilehash: 49db3a784234daee807465fce63fa7446fddef12
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2018
ms.locfileid: "35703823"
---
# <a name="sqlpackageexe"></a>SqlPackage.exe
**SqlPackage.exe** 是命令列公用程式，可自動化下列資料庫開發工作：  
  
-   [Extract](#help-for-the-extract-action)：從即時的 SQL Server 或 Azure SQL Database 建立資料庫快照集 (.dacpac) 檔案。  
  
-   [Publish](#publish-parameters-properties-and-sqlcmd-variables)：累加更新資料庫結構描述以符合來源 .dacpac 檔案的結構描述。 如果資料庫不存在伺服器上，發行作業會建立資料庫。 否則，將更新現有的資料庫。  
  
-   [Export](#export-parameters-and-properties)：將即時資料庫 (包括資料庫結構描述和使用者資料) 從 SQL Server 或 Azure SQL Database 匯出到 BACPAC 套件 (.bacpac 檔案)。  
  
-   [Import](#import-parameters-and-properties)：將結構描述和資料表資料從 BACPAC 套件匯入至 SQL Server 或 Azure SQL Database 執行個體中的新使用者資料庫。  
  
-   [DeployReport](#deployreport-parameters-and-properties)：建立發行動作所做變更的 XML 報表。  
  
-   [DriftReport](#driftreport-parameters)：建立自從上次註冊以來已經對註冊資料庫所做變更的 XML 報表。  
  
-   [Script](#script-parameters-and-properties)：建立 Transact-SQL 累加更新指令碼，這個指令碼會更新目標的結構描述以符合來源的結構描述。  
  
**SqlPackage.exe** 命令列可讓您指定這些動作以及動作特有的參數和屬性。  
  
## <a name="command-line-syntax"></a>命令列語法  
**SqlPackage.exe** 會使用命令列上指定的參數、屬性和 SQLCMD 變數來起始指定的動作。  
  
```  
SqlPackage {parameters}{properties}{SQLCMD Variables}  
```  
  
   
 
### <a name="help-for-the-extract-action"></a>Extract 動作的說明。
|參數|簡短形式|ReplTest1|描述|
|---|---|---|---|
|**/Action:**|**/a**|Extract|指定要執行的動作。 |
|**/ OverwriteFiles:**|**/of**|{True&#124;False}|指定 sqlpackage.exe 是否應該覆寫現有的檔案。 指定 false 會導致 sqlpackage.exe 在遇到現有的檔案時中止動作。 預設值是 True。 |
|**/Properties:**|**/p**|{PropertyName}={Value}|指定動件特有屬性的名稱/值組：{PropertyName}={Value}。 請參閱特定動作的說明，以便查看該動作的屬性名稱。 範例： sqlpackage.exe /Action： 發行 /？。 |
|**/Quiet:**|**/q**|{True&#124;False}|指定是否隱藏詳細的意見反應。 預設為 False。 |
|**/ SourceConnectionString:**|**/scs**|{string}|指定來源資料庫的有效 SQL Server/Azure 連接字串。 如果指定了此參數，就應該以獨佔方式將它用於所有其他來源參數。 |
|**/SourceDatabaseName:**|**/sdn**|{string}|定義來源資料庫的名稱。 |
|**/ SourceEncryptConnection:**|**/sec**|{True&#124;False}|指定 SQL 加密是否應該用於來源資料庫連接。 |
|**/SourcePassword:**|**/sp**|{string}|若為 SQL Server 驗證案例，則定義要用來存取來源資料庫的密碼。 |
|**/ SourceServerName:**|**/ssn**|{string}|定義裝載來源資料庫的伺服器名稱。 |
|**/ SourceTimeout:**|**/st**|{int}|指定建立來源資料庫連線的逾時 (以秒為單位)。 |
|**/ SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|指定是否要使用 SSL 來加密來源資料庫連線並且略過驗證信任的憑證鏈結。 |
|**/SourceUser:**|**/su**|{string}|若為 SQL Server 驗證案例，則定義要用來存取來源資料庫的 SQL Server 使用者。 |
|**/TargetFile:**|**/tf**|{string}| 指定要做為目標的動作，而不是資料庫的目標檔案 （亦即.dacpac 檔案）。 如果使用此參數，其他目標參數都應該無效。 這個參數應該是僅支援資料庫目標的動作無效。| 
|**/ TenantId:**|**/tid**|{string}|代表 Azure AD 租用戶識別碼或網域名稱。 此選項，才可支援客體或匯入 Azure AD 使用者，以及 Microsoft 帳戶，例如 outlook.com、 hotmail.com 或 live.com。 如果省略這個參數，則 Azure AD 的預設租用戶識別碼會使用，假設已驗證的使用者是此 ad 原生的使用者。 不過，在此情況下任何客體或匯入的使用者和/或裝載於此 Azure AD 的 Microsoft 帳戶不支援，而且此作業會失敗。 <br/> 如需 Active Directory 通用驗證的詳細資訊，請參閱[通用驗證與 SQL Database 和 SQL 資料倉儲 （SSMS 支援 MFA）](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)。|
|**/ UniversalAuthentication:**|**/ua**|{True&#124;False}|指定是否應該使用通用驗證。 設為 True 時，互動式驗證通訊協定已啟用支援 MFA。 此選項也可以用於 Azure AD 驗證，而不使用互動式要求使用者輸入其使用者名稱和密碼或整合式的驗證 （Windows 認證） 通訊協定的 MFA。 SourceConnectionString 時 /UniversalAuthentication 設為 True 時，可以指定沒有 Azure AD 驗證 (/ scs)。 SourceConnectionString 當 /UniversalAuthentication 設定為 False 時，必須指定 Azure AD 驗證 (/ scs)。 <br/> 如需 Active Directory 通用驗證的詳細資訊，請參閱[通用驗證與 SQL Database 和 SQL 資料倉儲 （SSMS 支援 MFA）](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)。|

### <a name="properties-specific-to-the-extract-action"></a>Extract 動作的特定屬性：
|屬性|ReplTest1|描述|
|---|---|---|
|**/p:**|CommandTimeout = (INT32 '60')|以秒為單位指定對 SQL Server 執行查詢時的命令逾時。|
|**/p:**|DacApplicationDescription=(STRING)|定義要儲存在 DACPAC 中繼資料中的應用程式描述。|
|**/p:**|DacApplicationName=(STRING)|定義要儲存在 DACPAC 中繼資料中的應用程式名稱。 預設值為資料庫名稱。|
|**/p:**|DacMajorVersion = (INT32 '1')|定義要儲存在 DACPAC 中繼資料中的主要版本。|
|**/p:**|DacMinorVersion = (INT32 '0')|定義要儲存在 DACPAC 中繼資料中的次要版本。|
|**/p:**|ExtractAllTableData=(BOOLEAN)|指出是否擷取了所有使用者資料表的資料。 如果為 'true'，擷取所有使用者資料表的資料時，，而且您無法指定個別使用者資料表擷取資料。 如果為 'false'，指定要從中擷取資料的一或多個使用者資料表。|
|**/p:**|ExtractApplicationScopedObjectsOnly = (布林值 ' True')|如果為 true，則只擷取指定之來源的應用程式範圍物件。 如果為 false，則擷取指定之來源的所有物件。|
|**/p:**|ExtractReferencedServerScopedElements = (布林值 ' True')|若為 true，則擷取來源資料庫物件所參考的登入、伺服器稽核及認證物件。|
|**/p:**|ExtractUsageProperties=(BOOLEAN)|指定是否會從資料庫擷取用法屬性，例如資料表資料列計數和索引大小。|
|**/p:**|IgnoreExtendedProperties=(BOOLEAN)|指定是否應該忽略擴充屬性。|
|**/p:**|IgnorePermissions = (布林值 ' True')|指定是否應該忽略權限。|
|**/p:**|IgnoreUserLoginMappings=(BOOLEAN)|指定是否忽略使用者與登入之間的關聯性。|
|**/p:**|儲存體 = ({檔案&#124;記憶體} 'File')|指定支援儲存體的類型，以供結構描述模型在擷取期間使用。|
|**/p:**|TableData=(STRING)|指出擷取資料的資料表。 指定資料表名稱，含方括號名稱部分，以下列格式： schema_name.table_identifier。|
|**/p:**|VerifyExtraction=(BOOLEAN)|指定是否應該驗證擷取的 dacpac。|

## <a name="publish-parameters-properties-and-sqlcmd-variables"></a>Publish 參數、屬性與 SQLCMD 變數  
SqlPackage.exe 發行作業會累加更新目標資料庫的結構描述，使其符合來源資料庫的結構。 發行部署套件時，若其中包含所有資料表或資料表子集的使用者資料，則除了結構描述以外，也會更新資料表資料。 請注意，資料部署將覆寫目標資料庫之現有資料表中的結構描述和資料。 對於未包括在部署套件的資料表，資料部署將不會變更目標資料庫中的現有結構描述或資料。  
  

### <a name="help-for-publish-action"></a>發行動作的說明。
|參數|簡短形式|ReplTest1|描述|
|---|---|---|---|
|**/Action:**|**/a**|發行|指定要執行的動作。 |
|**/ AzureKeyVaultAuthMethod:**|**/akv**|{互動式&#124;ClientIdSecret}|指定存取 Azure Key Vault 時要使用的驗證方法 |
|**/ClientId:**|**/cid**|{string}|指定必要時驗證 Azure Key Vault 所要使用的用戶端識別碼 |
|**/ OverwriteFiles:**|**/of**|{True&#124;False}|指定 sqlpackage.exe 是否應該覆寫現有的檔案。 指定 false 會導致 sqlpackage.exe 在遇到現有的檔案時中止動作。 預設值是 True。 |
|**/Profile:**|**/pr**|{string}|指定 DAC 發行設定檔的檔案路徑。 設定檔會定義產生輸出時要使用之屬性及變數的集合。|
|**/Properties:**|**/p**|{PropertyName}={Value}|指定動件特定屬性的名稱/值對：{PropertyName}={Value}。 請參閱特定動作的說明，以便查看該動作的屬性名稱。 範例： sqlpackage.exe /Action： 發行 /？。|
|**/Quiet:**|**/q**|{True&#124;False}|指定是否隱藏詳細的意見反應。 預設為 False。|
|**/Secret:**|**/secr**|{string}|指定必要時驗證 Azure Key Vault 所要使用的用戶端密碼 |
|**/ SourceConnectionString:**|**/scs**|{string}|指定來源資料庫的有效 SQL Server/Azure 連接字串。 如果指定了此參數，就應該以獨佔方式將它用於所有其他來源參數。 |
|**/SourceDatabaseName:**|**/sdn**|{string}|定義來源資料庫的名稱。 |
|**/ SourceEncryptConnection:**|**/sec**|{True&#124;False}|指定 SQL 加密是否應該用於來源資料庫連接。 |
|**/Sourcefile:**|**/sf**|{string}|指定要當作動作來源使用的來源檔案，而非資料庫。 如果使用了此參數，其他來源參數都應該無效。 |
|**/SourcePassword:**|**/sp**|{string}|若為 SQL Server 驗證案例，則定義要用來存取來源資料庫的密碼。 |
|**/ SourceServerName:**|**/ssn**|{string}|定義裝載來源資料庫的伺服器名稱。 |
|**/ SourceTimeout:**|**/st**|{int}|指定建立來源資料庫連線的逾時 (以秒為單位)。 |
|**/ SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|指定是否要使用 SSL 來加密來源資料庫連線並且略過驗證信任的憑證鏈結。 |
|**/SourceUser:**|**/su**|{string}|若為 SQL Server 驗證案例，則定義要用來存取來源資料庫的 SQL Server 使用者。 |
|**/ TargetConnectionString:**|**/tcs**|{string}|指定目標資料庫的有效 SQL Server/Azure 連接字串。 如果指定此參數，就應該以獨佔方式將它用於所有其他目標參數。 |
|**/TargetDatabaseName:**|**/tdn**|{string}|指定 sqlpackage.exe 動作目標之資料庫名稱的覆寫。 |
|**/ TargetEncryptConnection:**|**/tec**|{True&#124;False}|指定 SQL 加密是否應該用於目標資料庫連線。 |
|**/ TargetPassword:**|**/tp**|{string}|若為 SQL Server 驗證案例，則定義要用來存取目標資料庫的密碼。 |
|**/ TargetServerName:**|**/tsn**|{string}|定義裝載目標資料庫的伺服器名稱。 |
|**/ TargetTimeout:**|**/tt**|{int}|指定建立目標資料庫連線的逾時 (以秒為單位)。 Azure AD 中，建議您使用這個值是大於或等於為 30 秒。|
|**/ TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|指定是否要使用 SSL 來加密目標資料庫連線並略過驗證信任的憑證鏈結。 |
|**/ TargetUser:**|**/tu**|{string}|若為 SQL Server 驗證案例，則定義要用以存取目標資料庫的 SQL Server 使用者。 |
|**/ TenantId:**|**/tid**|{string}|代表 Azure AD 租用戶識別碼或網域名稱。 此選項，才可支援客體或匯入 Azure AD 使用者，以及 Microsoft 帳戶，例如 outlook.com、 hotmail.com 或 live.com。 如果省略這個參數，則 Azure AD 的預設租用戶識別碼會使用，假設已驗證的使用者是此 ad 原生的使用者。 不過，在此情況下任何客體或匯入的使用者和/或裝載於此 Azure AD 的 Microsoft 帳戶不支援，而且此作業會失敗。 <br/> 如需 Active Directory 通用驗證的詳細資訊，請參閱[通用驗證與 SQL Database 和 SQL 資料倉儲 （SSMS 支援 MFA）](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)。|
|**/ UniversalAuthentication:**|**/ua**|{True&#124;False}|指定是否應該使用通用驗證。 設為 True 時，互動式驗證通訊協定已啟用支援 MFA。 此選項也可以用於 Azure AD 驗證，而不使用互動式要求使用者輸入其使用者名稱和密碼或整合式的驗證 （Windows 認證） 通訊協定的 MFA。 SourceConnectionString 時 /UniversalAuthentication 設為 True 時，可以指定沒有 Azure AD 驗證 (/ scs)。 SourceConnectionString 當 /UniversalAuthentication 設定為 False 時，必須指定 Azure AD 驗證 (/ scs)。 <br/> 如需 Active Directory 通用驗證的詳細資訊，請參閱[通用驗證與 SQL Database 和 SQL 資料倉儲 （SSMS 支援 MFA）](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)。|
|**/Variables:**|**/v**|{PropertyName}={Value}|指定動件特定變數的名稱/值對：{VariableName}={Value}。 DACPAC 檔案包含有效 SQLCMD 變數的清單。 如果未針對每一個變數提供值，則將產生錯誤。 |

### <a name="properties-specific-to-the-publish-action"></a>發行動作的特定屬性：
|屬性|ReplTest1|描述|
|---|---|---|
|**/p:**|AdditionalDeploymentContributorArguments=(STRING)|為部署參與者指定其他部署參與者引數。 這應該是以分號區隔的值清單。|
|**/p:**|AdditionalDeploymentContributors=(STRING)|指定部署 dacpac 時應該執行的其他部署參與者。 這應該是以分號區隔的完整組建參與者名稱或識別碼清單。|
|**/p:**|AllowDropBlocking Assemblies=(BOOLEAN)|這個屬性是供 SqlClr 部署用來使任何封鎖的組件會在部署計畫中卸除。 根據預設，如果必須卸除任何參考組件，則該封鎖/參考組件會封鎖組件更新。|
|**/p:**|AllowIncompatiblePlatform=(BOOLEAN)|指定儘管 SQL Server 平台不相容，是否仍要嘗試動作。|
|**/p:**|AllowUnsafeRowLevelSecurityDataMovement=(BOOLEAN)|若此屬性設定為 true，請勿封鎖具有資料列層級安全性之資料表的資料動作。 預設值為 false。|
|**/p:**|BackupDatabaseBeforeChanges=(BOOLEAN)|在部署任何變更之前，先備份資料庫。|
|**/p:**|BlockOnPossibleDataLoss = (布林值 ' True')|指定如果發行作業可能導致資料遺失，就應該終止發行事件。|
|**/p:**|BlockWhenDriftDetected = (布林值 ' True')|指定是否封鎖更新結構描述不再符合註冊或已取消註冊的資料庫。|
|**/p:**|CommandTimeout = (INT32 '60')|以秒為單位指定對 SQL Server 執行查詢時的命令逾時。|
|**/p:**|CommentOutSetVarDeclarations=(BOOLEAN)|指定在產生的發行指令碼中是否應該將 SETVAR 變數的宣告標記為註解。 如果您計畫在使用 SQLCMD.EXE 等工具進行發行時在命令列指定值，就可以選擇這種作法。|
|**/p:**|CompareUsingTargetCollation=(BOOLEAN)|這個設定表示資料庫的定序於部署期間的處理方式。如果目標資料庫的定序不符合來源所指定的定序，預設會更新目標資料庫的定序。 當設定這個選項時，則應該使用目標資料庫 (或伺服器) 的定序。|
|**/p:**|CreateNewDatabase=(BOOLEAN)|指定當您發行至資料庫時，應該更新目標資料庫或應該卸除並重新建立目標資料庫。|
|**/p:**|DatabaseEdition = ({Basic&#124;標準&#124;Premium&#124;預設} 'Default')|定義 Azure SQL Database 的版本。|
|**/p:**|DatabaseMaximumSize=(INT32)|定義 Azure SQL Database 的大小上限 (以 GB 表示)。|
|**/p:**|DatabaseServiceObjective=(STRING)|定義 Azure SQL Database 的效能等級，例如 "P0" 或 "S1"。|
|**/p:**|DeployDatabaseInSingleUserMode=(BOOLEAN)|若為 true，則資料庫會在設定為單一使用者模式後部署。|
|**/p:**|DisableAndReenableDdlTriggers = (布林值 ' True')|指定是否在發行程序開始時停用資料定義語言 (DDL) 觸發程序，並在發行動作結束時重新啟用。|
|**/p:**|DoNotAlterChangeDataCaptureObjects = (布林值 ' True')|如果為 true，則不會改變異動資料擷取物件。|
|**/p:**|DoNotAlterReplicatedObjects = (布林值 ' True')|指定驗證期間是否識別有複寫的物件。|
|**/p:**|DoNotDropObjectType=(STRING)|物件型別時不應捨棄當 DropObjectsNotInSource 為 true。 有效物件類型名稱為 Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers。|
|**/p:**|DoNotDropObjectTypes=(STRING)|當 DropObjectsNotInSource 為 true 時不應捨棄的分號分隔物件類型清單。 有效的物件類型名稱為 Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers。|
|**/p:**|DropConstraintsNotInSource = (布林值 ' True')|指定當您發行至資料庫時，是否要從目標資料庫中卸除不存在資料庫快照集 (.dacpac) 檔案中的條件約束。|
|**/p:**|DropDmlTriggersNotInSource = (布林值 ' True')|指定當您發行至資料庫時，是否要從目標資料庫中卸除不存在資料庫快照集 (.dacpac) 檔案中的 DML 觸發程序。|
|**/p:**|DropExtendedPropertiesNotInSource = (布林值 ' True')|指定當您發行至資料庫時，是否要從目標資料庫中卸除不存在資料庫快照集 (.dacpac) 檔案中的擴充屬性。|
|**/p:**|DropIndexesNotInSource = (布林值 ' True')|指定當您發行至資料庫時，是否要從目標資料庫中卸除不存在資料庫快照集 (.dacpac) 檔案中的索引。|
|**/p:**|DropObjectsNotInSource=(BOOLEAN)|指定當您發行至資料庫時，是否要從目標資料庫中卸除不存在資料庫快照集 (.dacpac) 檔案中的物件。 此值的優先順序高過 DropExtendedProperties。|
|**/p:**|DropPermissionsNotInSource=(BOOLEAN)|指定當您發行更新至資料庫時，是否要從目標資料庫中卸除不存在資料庫快照集 (.dacpac) 檔案中的權限。|
|**/p:**|DropRoleMembersNotInSource=(BOOLEAN)|指定當您發行更新至資料庫時，是否要從目標資料庫中卸除資料庫快照集 (.dacpac) 檔案中沒有定義的角色成員。|
|**/p:**|DropStatisticsNotInSource = (布林值 ' True')|指定當您發行至資料庫時，是否要從目標資料庫卸除不存在於資料庫快照集 (.dacpac) 檔案中的統計資料。|
|**/p:**|ExcludeObjectType=(STRING)|部署期間應該忽略的物件類型。 有效物件類型名稱為 Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers。|
|**/p:**|ExcludeObjectTypes=(STRING)|以分號區隔的物件類型清單，列出部署期間應該忽略的物件類型。 有效的物件類型名稱為 Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers。|
|**/p:**|GenerateSmartDefaults=(BOOLEAN)|在更新含有資料且資料行不允許 null 值的資料表時，自動提供預設值。|
|**/p:**|IgnoreAnsiNulls = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新 ANSI NULLS 設定的差異。|
|**/p:**|IgnoreAuthorizer=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新授權者的差異。|
|**/p:**|IgnoreColumnCollation=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新資料行定序的差異。|
|**/p:**|IgnoreComments=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新註解的差異。|
|**/p:**|IgnoreCryptographicProviderFilePath = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新密碼編譯提供者之檔案路徑的差異。|
|**/p:**|IgnoreDdlTriggerOrder=(BOOLEAN)|指定當您發行至資料庫或伺服器時，應該忽略或更新資料定義語言 (Data Definition Language) (DDL) 觸發程序的順序差異。|
|**/p:**|IgnoreDdlTriggerState=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新資料定義語言 (Data Definition Language) (DDL) 觸發程序之啟用或停用狀態的差異。|
|**/p:**|IgnoreDefaultSchema=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新預設結構描述的差異。|
|**/p:**|IgnoreDmlTriggerOrder=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新資料操作語言 (DML) 觸發程序的順序差異。|
|**/p:**|IgnoreDmlTriggerState=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新 DML 觸發程序之啟用或停用狀態的差異。|
|**/p:**|IgnoreExtendedProperties=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新擴充屬性的差異。|
|**/p:**|IgnoreFileAndLogFilePath = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新檔案和記錄檔之路徑的差異。|
|**/p:**|IgnoreFilegroupPlacement = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新 FILEGROUP 中物件位置的差異。|
|**/p:**|IgnoreFileSize = (布林值 ' True')|指定當您發行至資料庫時，應該忽略檔案大小的差異或應該發出警告。|
|**/p:**|IgnoreFillFactor = (布林值 ' True')|指定當您發行至資料庫時，應該忽略索引儲存體之填滿因數的差異或應該發出警告。|
|**/p:**|IgnoreFullTextCatalogFilePath = (布林值 ' True')|指定當您發行至資料庫時，應該忽略全文檢索目錄之檔案路徑的差異或應該發出警告。|
|**/p:**|IgnoreIdentitySeed=(BOOLEAN)|指定當您發行更新至資料庫時，應該忽略或更新識別欄位之種子的差異。|
|**/p:**|IgnoreIncrement=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新識別欄位之增量的差異。|
|**/p:**|IgnoreIndexOptions=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新索引選項的差異。|
|**/p:**|IgnoreIndexPadding = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新索引填補的差異。|
|**/p:**|IgnoreKeywordCasing = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新關鍵字之大小寫的差異。|
|**/p:**|IgnoreLockHintsOnIndexes=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新索引之鎖定提示的差異。|
|**/p:**|IgnoreLoginSids = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新安全性識別碼 (SID) 的差異。|
|**/p:**|IgnoreNotForReplication=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新不可複寫設定。|
|**/p:**|IgnoreObjectPlacementOnPartitionScheme = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新物件在資料分割配置上的位置。|
|**/p:**|IgnorePartitionSchemes=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新資料分割配置和函式的差異。|
|**/p:**|IgnorePermissions=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新權限的差異。|
|**/p:**|IgnoreQuotedIdentifiers = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新引號識別項設定的差異。|
|**/p:**|IgnoreRoleMembership=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新登入之角色成員資格的差異。|
|**/p:**|IgnoreRouteLifetime = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新 SQL Server 將路由保留在路由表中之時間長短的差異。|
|**/p:**|IgnoreSemicolonBetweenStatements = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新 T-SQL 陳述式間之分號的差異。|
|**/p:**|IgnoreTableOptions=(BOOLEAN)|指定當您發行至資料庫時，將忽略或更新資料表選項的差異。|
|**/p:**|IgnoreUserSettingsObjects=(BOOLEAN)|指定當您發行至資料庫時，將忽略或更新使用者設定物件的差異。|
|**/p:**|IgnoreWhitespace = (布林值 ' True')|指定當您發行至資料庫時，將忽略或更新空白字元的差異。|
|**/p:**|IgnoreWithNocheckOnCheckConstraints=(BOOLEAN)|指定當您發行至資料庫時，將忽略或更新檢查條件約束之 WITH NOCHECK 子句值的差異。|
|**/p:**|IgnoreWithNocheckOnForeignKeys=(BOOLEAN)|指定當您發行至資料庫時，將忽略或更新外部索引鍵之 WITH NOCHECK 子句值的差異。|
|**/p:**|IncludeCompositeObjects=(BOOLEAN)|將所有複合項目包含在單一發行作業中。|
|**/p:**|IncludeTransactionalScripts=(BOOLEAN)|指定當您發行至資料庫時，是否應該盡可能使用交易陳述式。|
|**/p:**|NoAlterStatementsToChangeClrTypes=(BOOLEAN)|指定發行在發現差異時一定要卸除並重新建立組件，而不是發出 ALTER ASSEMBLY 陳述式。|
|**/p:**|PopulateFilesOnFileGroups = (布林值 ' True')|指定在目標資料庫中建立新 FileGroup 時，是否一併建立新檔案。|
|**/p:**|RegisterDataTierApplication=(BOOLEAN)|指定結構描述是否向資料庫伺服器註冊。|
|**/p:**|RunDeploymentPlanExecutors=(BOOLEAN)|指定執行其他作業時，是否應該執行 DeploymentPlanExecutor 參與者。|
|**/p:**|ScriptDatabaseCollation=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新資料庫定序的差異。|
|**/p:**|ScriptDatabaseCompatibility=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新資料庫相容性的差異。|
|**/p:**|ScriptDatabaseOptions = (布林值 ' True')|指定是否應該在發行動作中設定或更新目標資料庫屬性。|
|**/p:**|ScriptDeployStateChecks=(BOOLEAN)|指定是否在發行指令碼中產生陳述式，來驗證資料庫名稱和伺服器名稱是否符合資料庫專案中指定的名稱。|
|**/p:**|ScriptFileSize=(BOOLEAN)|控制將檔案加入至檔案群組時是否指定大小。|
|**/p:**|ScriptNewConstraintValidation = (布林值 ' True')|在發行結束的所有條件約束會驗證當做單一集合，避免檢查或 themiddle 發行的外部索引鍵條件約束導致資料錯誤。 如果設定為 False，您的條件約束會 publishedwithout 檢查對應的資料。|
|**/p:**|ScriptRefreshModule = (布林值 ' True')|在發行指令碼的結尾包含重新整理陳述式。|
|**/p:**|儲存體 = ({檔案&#124;記憶體})|指定在建置資料庫模型時，如何儲存項目。 基於效能考量，預設值為 InMemory。 若大型資料庫，則需要 File-backed 儲存體。|
|**/p:**|TreatVerificationErrorsAsWarnings=(BOOLEAN)|指定是否發行期間發生的錯誤驗證應 betreated 為警告。 Generateddeployment 計劃執行檢查，才能針對您的目標資料庫執行計畫。計畫驗證會偵測問題，例如遺失的僅限目標物件 （例如索引），進行變更，必須先卸除。 驗證也會偵測情況下，複合專案中，以參考的相依性 （例如資料表或檢視表） existbecause 但不存在於 thetarget 資料庫。 您可能選擇這樣做可以取得 allissues，而不需要第一個錯誤時停止發行動作的完整清單。|**/p:**|UnmodifiableObjectWarnings = (布林值 ' True')|指定在無法修改的物件中發現差異時 (例如檔案的檔案大小或檔案路徑不同) 是否應該產生警告。|
|**/p:**|VerifyCollationCompatibility = (布林值 ' True')|指定是否驗證定序相容性。|
|**/p:**|VerifyDeployment = (布林值 ' True')|指定是否應該在發行前執行檢查，以便在出現阻止發行成功的問題時停止發行動作。 例如，如果目標資料庫的外部索引鍵不存在資料庫專案中，因而在您發行時造成錯誤，則發行動作可能會停止。|
|
### <a name="sqlcmd-variables"></a>SQLCMD 變數  
下表描述可用來覆寫在發行動作期間所用 SQL 命令 (**sqlcmd**) 變數值之選項的格式。 命令列上指定的變數值會覆寫指派給變數的其他值 (例如在發行設定檔中)。  
  
|參數|預設|描述|  
|-------------|-----------|---------------|  
|**/ 變數: {PropertyName} = {Value}**||指定動件特有變數的名稱/值組：{VariableName}={Value}。 DACPAC 檔案包含有效 SQLCMD 變數的清單。 如果未針對每一個變數提供值，則將產生錯誤。|  
  
## <a name="export-parameters-and-properties"></a>匯出參數與屬性  
SqlPackage.exe 匯出動作會將即時資料庫從 SQL Server 或 Azure SQL Database 匯出到 BACPAC 套件 （.bacpac 檔案）。 依預設，所有資料表的資料將包括在 .bacpac 檔案中。 您可以選擇性地只指定要匯出資料的資料表子集。 驗證 Export 動作，可確保 Azure SQL Database 相容於完整目標資料庫，即使已指定資料表子集進行匯出也一樣。  
  
### <a name="help-for-export-action"></a>匯出動作的說明。
|參數|簡短形式|ReplTest1|描述|
|---|---|---|---|
|**/Action:**|**/a**|匯出|指定要執行的動作。 |
|**/ OverwriteFiles:**|**/of**|{True&#124;False}|指定 sqlpackage.exe 是否應該覆寫現有的檔案。 指定 false 會導致 sqlpackage.exe 在遇到現有的檔案時中止動作。 預設值是 True。 |
|**/Properties:**|**/p**|{PropertyName}={Value}|指定動件特定屬性的名稱/值對：{PropertyName}={Value}。 請參閱特定動作的說明，以便查看該動作的屬性名稱。 範例： sqlpackage.exe /Action： 發行 /？。|
|**/Quiet:**|**/q**|{True&#124;False}|指定是否隱藏詳細的意見反應。 預設為 False。|
|**/ SourceConnectionString:**|**/scs**|{string}|指定來源資料庫的有效 SQL Server/Azure 連接字串。 如果指定此參數，就應該以獨佔方式將它用於所有其他來源參數。 |
|**/SourceDatabaseName:**|**/sdn**|{string}|定義來源資料庫的名稱。 |
|**/ SourceEncryptConnection:**|**/sec**|{True&#124;False}|指定 SQL 加密是否應該用於來源資料庫連線。 |
|**/SourcePassword:**|**/sp**|{string}|若為 SQL Server 驗證案例，則定義要用來存取來源資料庫的密碼。 |
|**/ SourceServerName:**|**/ssn**|{string}|定義裝載來源資料庫的伺服器名稱。 |
|**/ SourceTimeout:**|**/st**|{int}|指定建立來源資料庫連線的逾時 (以秒為單位)。 |
|**/ SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|指定是否要使用 SSL 來加密來源資料庫連線並且略過驗證信任的憑證鏈結。 |
|**/SourceUser:**|**/su**|{string}|若為 SQL Server 驗證案例，則定義要用來存取來源資料庫的 SQL Server 使用者。 |
|**/TargetFile:**|**/tf**|{string}| 指定要做為 targetof 動作，而不是資料庫的目標檔案 （亦即.dacpac 檔案）。 如果使用此參數，其他目標參數都應該無效。 這個參數應該是無效的 foractions 僅支援資料庫目標。|
|**/ TenantId:**|**/tid**|{string}|代表 Azure AD 租用戶識別碼或網域名稱。 此選項，才可支援客體或匯入 Azure AD 使用者，以及 Microsoft 帳戶，例如 outlook.com、 hotmail.com 或 live.com。 如果省略這個參數，則 Azure AD 的預設租用戶識別碼會使用，假設已驗證的使用者是此 ad 原生的使用者。 不過，在此情況下任何客體或匯入的使用者和/或裝載於此 Azure AD 的 Microsoft 帳戶不支援，而且此作業會失敗。 <br/> 如需 Active Directory 通用驗證的詳細資訊，請參閱[通用驗證與 SQL Database 和 SQL 資料倉儲 （SSMS 支援 MFA）](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)。|
|**/ UniversalAuthentication:**|**/ua**|{True&#124;False}|指定是否應該使用通用驗證。 設為 True 時，互動式驗證通訊協定已啟用支援 MFA。 此選項也可以用於 Azure AD 驗證，而不使用互動式要求使用者輸入其使用者名稱和密碼或整合式的驗證 （Windows 認證） 通訊協定的 MFA。 SourceConnectionString 時 /UniversalAuthentication 設為 True 時，可以指定沒有 Azure AD 驗證 (/ scs)。 SourceConnectionString 當 /UniversalAuthentication 設定為 False 時，必須指定 Azure AD 驗證 (/ scs)。 <br/> 如需 Active Directory 通用驗證的詳細資訊，請參閱[通用驗證與 SQL Database 和 SQL 資料倉儲 （SSMS 支援 MFA）](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)。|

### <a name="properties-specific-to-the-export-action"></a>匯出動作特有的屬性：
|屬性|ReplTest1|描述|
|---|---|---|
|**/p:**|CommandTimeout = (INT32 '60')|以秒為單位指定對 SQL Server 執行查詢時的命令逾時。|
|**/p:**|儲存體 = ({檔案&#124;記憶體} 'File')|指定支援儲存體的類型，以供結構描述模型在擷取期間使用。|
|**/p:**|TableData=(STRING)|指出擷取資料的資料表。 指定 tablename 有或沒有括弧名稱中的組件︰ 格式： schema_name.table_identifier。|
|**/p:**|TargetEngineVersion = ({預設&#124;最新&#124;V11&#124;V12} 「 最新 」)|指定預期的目標引擎版本。 此 affectswhether 允許支援的 Azure SQL Database serverswith V12 功能，例如記憶體最佳化的資料表，產生的 bacpac 中的物件中。|
|**/p:**|VerifyFullTextDocumentTypesSupported=(BOOLEAN)|指定是否要驗證 Microsoft Azure SQL Database v12 支援的全文檢索文件類型。|
  
## <a name="import-parameters-and-properties"></a>匯入參數與屬性  
SqlPackage.exe 匯入動作匯入結構描述和資料表資料從 BACPAC 封裝-.bacpac 檔案-SQL Server 中的新的或空白資料庫或 Azure SQL Database。 在對現有資料庫進行匯入作業時，目標資料庫不能包含任何使用者定義的結構描述物件。  
  
### <a name="help-for-command-actions"></a>命令動作的說明。
|參數|簡短形式|ReplTest1|描述|
|---|---|---|---|
|**/Action:**|**/a**|匯入|指定要執行的動作。 |
|**/Properties:**|**/p**|{PropertyName}={Value}|指定動件特定屬性的名稱/值對：{PropertyName}={Value}。 請參閱特定動作的說明，以便查看該動作的屬性名稱。 範例： sqlpackage.exe /Action： 發行 /？。|
|**/Quiet:**|**/q**|{True&#124;False}|指定是否隱藏詳細的意見反應。 預設為 False。|
|**/Sourcefile:**|**/sf**|{string}|指定要當作動作來源使用的來源檔案，而非資料庫。 如果使用此參數，其他來源參數都應該無效。 |
|**/ TargetConnectionString:**|**/tcs**|{string}|指定目標資料庫的有效 SQL Server/Azure 連接字串。 如果指定此參數，就應該以獨佔方式將它用於所有其他目標參數。 |
|**/TargetDatabaseName:**|**/tdn**|{string}|指定 sqlpackage.exe 動作目標之資料庫名稱的覆寫。 |
|**/ TargetEncryptConnection:**|**/tec**|{True&#124;False}|指定 SQL 加密是否應該用於目標資料庫連線。 |
|**/ TargetPassword:**|**/tp**|{string}|若為 SQL Server 驗證案例，則定義要用來存取目標資料庫的密碼。 |
|**/ TargetServerName:**|**/tsn**|{string}|定義裝載目標資料庫的伺服器名稱。 |
|**/ TargetTimeout:**|**/tt**|{int}|指定建立目標資料庫連線的逾時 (以秒為單位)。 Azure AD 中，建議您使用這個值是大於或等於為 30 秒。|
|**/ TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|指定是否要使用 SSL 來加密目標資料庫連線並且略過驗證信任的憑證鏈結。 |
|**/ TargetUser:**|**/tu**|{string}|若為 SQL Server 驗證案例，則定義要用以存取目標資料庫的 SQL Server 使用者。 |
|**/ TenantId:**|**/tid**|{string}|代表 Azure AD 租用戶識別碼或網域名稱。 此選項，才可支援客體或匯入 Azure AD 使用者，以及 Microsoft 帳戶，例如 outlook.com、 hotmail.com 或 live.com。 如果省略這個參數，則 Azure AD 的預設租用戶識別碼會使用，假設已驗證的使用者是此 ad 原生的使用者。 不過，在此情況下任何客體或匯入的使用者和/或裝載於此 Azure AD 的 Microsoft 帳戶不支援，而且此作業會失敗。 <br/> 如需 Active Directory 通用驗證的詳細資訊，請參閱[通用驗證與 SQL Database 和 SQL 資料倉儲 （SSMS 支援 MFA）](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)。|
|**/ UniversalAuthentication:**|**/ua**|{True&#124;False}|指定是否應該使用通用驗證。 設為 True 時，互動式驗證通訊協定已啟用支援 MFA。 此選項也可以用於 Azure AD 驗證，而不使用互動式要求使用者輸入其使用者名稱和密碼或整合式的驗證 （Windows 認證） 通訊協定的 MFA。 SourceConnectionString 時 /UniversalAuthentication 設為 True 時，可以指定沒有 Azure AD 驗證 (/ scs)。 SourceConnectionString 當 /UniversalAuthentication 設定為 False 時，必須指定 Azure AD 驗證 (/ scs)。 <br/> 如需 Active Directory 通用驗證的詳細資訊，請參閱[通用驗證與 SQL Database 和 SQL 資料倉儲 （SSMS 支援 MFA）](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)。|

匯入動作特有的屬性：
|屬性|ReplTest1|描述|
|---|---|---|
|**/p:**|CommandTimeout = (INT32 '60')|以秒為單位指定對 SQL Server 執行查詢時的命令逾時。|
|**/p:**|DatabaseEdition = ({Basic&#124;標準&#124;Premium&#124;預設} 'Default')|定義 Azure SQL Database 的版本。|
|**/p:**|DatabaseMaximumSize=(INT32)|定義 Azure SQL Database 的大小上限 (以 GB 表示)。|
|**/p:**|DatabaseServiceObjective=(STRING)|定義 Azure SQL Database 的效能等級，例如 "P0" 或 "S1"。|
|**/p:**|ImportContributorArguments=(STRING)|指定部署參與者的部署參與者引數。 這應該是以分號區隔的值清單。|
|**/p:**|ImportContributors=(STRING)|指定應該執行時的部署參與者 bacpac isimported。 這應該是以分號區隔的完整組建參與者名稱或識別碼清單。|
|**/p:**|儲存體 = ({檔案&#124;記憶體})|指定在建置資料庫模型時，如何儲存項目。 基於效能考量，預設值為 InMemory。 若大型資料庫，則需要 File-backed 儲存體。|
  
## <a name="deployreport-parameters-and-properties"></a>DeployReport 參數與屬性  
**SqlPackage.exe** 報表動作會建立發行動作所做變更的 XML 報表。  
  
### <a name="help-for-deployreport-action"></a>DeployReport 動作的說明
|參數|簡短形式|ReplTest1|描述|
|---|---|---|---|
|**/Action:**|**/a**|DeployReport|指定要執行的動作。 |
|**/OutputPath:**|**/op**|{string}|指定輸出檔案產生位置的檔案路徑。 |
|**/ OverwriteFiles:**|**/of**|{True&#124;False}|指定 sqlpackage.exe 是否應該覆寫現有的檔案。 指定 false 會導致 sqlpackage.exe 在遇到現有的檔案時中止動作。 預設值是 True。 |
|**/Profile:**|**/pr**|{string}|指定 DAC 發行設定檔的檔案路徑。 設定檔會定義產生輸出時要使用之屬性及變數的集合。 |
|**/Properties:**|**/p**|{PropertyName}={Value}|指定動件特有屬性的名稱/值組：{PropertyName}={Value}。 請參閱特定動作的說明，以便查看該動作的屬性名稱。 範例： sqlpackage.exe /Action： 發行 /？。 |
|**/Quiet:**|**/q**|{True&#124;False}|指定是否隱藏詳細的意見反應。 預設為 False。 |
|**/ SourceConnectionString:**|**/scs**|{string}|指定來源資料庫的有效 SQL Server/Azure 連接字串。 如果指定了此參數，就應該以獨佔方式將它用於所有其他來源參數。 |
|**/SourceDatabaseName:**|**/sdn**|{string}|定義來源資料庫的名稱。 |
|**/ SourceEncryptConnection:**|**/sec**|{True&#124;False}|指定 SQL 加密是否應該用於來源資料庫連接。 |
|**/Sourcefile:**|**/sf**|{string}|指定要當作動作來源使用的來源檔案，而非資料庫。 如果使用了此參數，其他來源參數都應該無效。 |
|**/SourcePassword:**|**/sp**|{string}|若為 SQL Server 驗證案例，則定義要用來存取來源資料庫的密碼。 |
|**/ SourceServerName:**|**/ssn**|{string}|定義裝載來源資料庫的伺服器名稱。 |
|**/ SourceTimeout:**|**/st**|{int}|指定建立來源資料庫連線的逾時 (以秒為單位)。 |
|**/ SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|指定是否要使用 SSL 來加密來源資料庫連線並且略過驗證信任的憑證鏈結。 |
|**/SourceUser:**|**/su**|{string}|若為 SQL Server 驗證案例，則定義要用來存取來源資料庫的 SQL Server 使用者。 |
|**/ TargetConnectionString:**|**/tcs**|{string}|指定目標資料庫的有效 SQL Server/Azure 連接字串。 如果指定此參數，就應該以獨佔方式將它用於所有其他目標參數。 |
|**/TargetDatabaseName:**|**/tdn**|{string}|指定 sqlpackage.exe 動作目標之資料庫名稱的覆寫。 |
|**/ TargetEncryptConnection:**|**/tec**|{True&#124;False}|指定 SQL 加密是否應該用於目標資料庫連線。 |
|**/TargetFile:**|**/tf**|{string}|指定要做為目標的動作，而不是資料庫的目標檔案 （亦即.dacpac 檔案）。 如果使用此參數，其他目標參數都應該無效。 這個參數應該是僅支援資料庫目標的動作無效。|
|**/ TargetPassword:**|**/tp**|{string}|若為 SQL Server 驗證案例，則定義要用來存取目標資料庫的密碼。 |
|**/ TargetServerName:**|**/tsn**|{string}|定義裝載目標資料庫的伺服器名稱。 |
|**/ TargetTimeout:**|**/tt**|{int}|指定建立目標資料庫連線的逾時 (以秒為單位)。 Azure AD 中，建議您使用這個值是大於或等於為 30 秒。|
|**/ TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|指定是否要使用 SSL 來加密目標資料庫連線並略過驗證信任的憑證鏈結。 |
|**/ TargetUser:**|**/tu**|{string}|若為 SQL Server 驗證案例，則定義要用以存取目標資料庫的 SQL Server 使用者。 |
|**/ TenantId:**|**/tid**|{string}|代表 Azure AD 租用戶識別碼或網域名稱。 此選項，才可支援客體或匯入 Azure AD 使用者，以及 Microsoft 帳戶，例如 outlook.com、 hotmail.com 或 live.com。 如果省略這個參數，則 Azure AD 的預設租用戶識別碼會使用，假設已驗證的使用者是此 ad 原生的使用者。 不過，在此情況下任何客體或匯入的使用者和/或裝載於此 Azure AD 的 Microsoft 帳戶不支援，而且此作業會失敗。 <br/> 如需 Active Directory 通用驗證的詳細資訊，請參閱[通用驗證與 SQL Database 和 SQL 資料倉儲 （SSMS 支援 MFA）](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)。|
|**/ UniversalAuthentication:**|**/ua**|{True&#124;False}|指定是否應該使用通用驗證。 設為 True 時，互動式驗證通訊協定已啟用支援 MFA。 此選項也可以用於 Azure AD 驗證，而不使用互動式要求使用者輸入其使用者名稱和密碼或整合式的驗證 （Windows 認證） 通訊協定的 MFA。 SourceConnectionString 時 /UniversalAuthentication 設為 True 時，可以指定沒有 Azure AD 驗證 (/ scs)。 SourceConnectionString 當 /UniversalAuthentication 設定為 False 時，必須指定 Azure AD 驗證 (/ scs)。 <br/> 如需 Active Directory 通用驗證的詳細資訊，請參閱[通用驗證與 SQL Database 和 SQL 資料倉儲 （SSMS 支援 MFA）](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)。|
|**/Variables:**|**/v**|{PropertyName}={Value}|指定動件特有變數的名稱/值組：{VariableName}={Value}。 DACPAC 檔案包含有效 SQLCMD 變數的清單。 如果未針對每一個變數提供值，則將產生錯誤。 |

## <a name="properties-specific-to-the-deployreport-action"></a>DeployReport 動作特有的屬性：
|屬性|ReplTest1|描述|
|---|---|---|
|**/p:**|AdditionalDeploymentContributorArguments=(STRING)|為部署參與者指定其他部署參與者引數。 這應該是以分號區隔的值清單。|
|**/p:**|AdditionalDeploymentContributors=(STRING)|指定部署 dacpac 時應該執行的其他部署參與者。 這應該是以分號區隔的完整組建參與者名稱或識別碼清單。|
|**/p:**|AllowDropBlocking Assemblies=(BOOLEAN)|這個屬性是供 SqlClr 部署用來使任何封鎖的組件會在部署計畫中卸除。 根據預設，如果必須卸除任何參考組件，則該封鎖/參考組件會封鎖組件更新。|
|**/p:**|AllowIncompatiblePlatform=(BOOLEAN)|指定儘管 SQL Server 平台不相容，是否仍要嘗試動作。|
|**/p:**|AllowUnsafeRowLevelSecurityDataMovement=(BOOLEAN)|若此屬性設定為 true，請勿封鎖具有資料列層級安全性之資料表的資料動作。 預設值為 false。|
|**/p:**|BackupDatabaseBeforeChanges=(BOOLEAN)|在部署任何變更之前，先備份資料庫。|
|**/p:**|BlockOnPossibleDataLoss = (布林值 ' True')|指定如果發行作業可能導致資料遺失，就應該終止發行事件。|
|**/p:**|BlockWhenDriftDetected = (布林值 ' True')|指定是否封鎖更新結構描述不再符合註冊或已取消註冊的資料庫。 |
|**/p:**|CommandTimeout = (INT32 '60')|以秒為單位指定對 SQL Server 執行查詢時的命令逾時。 |
|**/p:**|CommentOutSetVarDeclarations=(BOOLEAN)|指定在產生的發行指令碼中是否應該將 SETVAR 變數的宣告標記為註解。 如果您計畫在使用 SQLCMD.EXE 等工具進行發行時在命令列指定值，就可以選擇這種作法。 |
|**/p:**|CompareUsingTargetCollation=(BOOLEAN)|這個設定表示資料庫的定序於部署期間的處理方式。如果目標資料庫的定序不符合來源所指定的定序，預設會更新目標資料庫的定序。 當設定這個選項時，則應該使用目標資料庫 (或伺服器) 的定序。 |
|**/p:**|CreateNewDatabase=(BOOLEAN)|指定當您發行至資料庫時，應該更新目標資料庫或應該卸除並重新建立目標資料庫。 |
|**/p:**|DatabaseEdition = ({Basic&#124;標準&#124;Premium&#124;預設} 'Default')|定義 Azure SQL Database 的版本。 |
|**/p:**|DatabaseMaximumSize=(INT32)|定義 Azure SQL Database 的大小上限 (以 GB 表示)。|
|**/p:**|DatabaseServiceObjective=(STRING)|定義 Azure SQL Database 的效能等級，例如 "P0" 或 "S1"。 |
|**/p:**|DeployDatabaseInSingleUserMode=(BOOLEAN)|若為 true，則資料庫會在設定為單一使用者模式後部署。 |
|**/p:**|DisableAndReenableDdlTriggers = (布林值 ' True')| 指定是否在發行程序開始時停用資料定義語言 (DDL) 觸發程序，並在發行動作結束時重新啟用。|
|**/p:**|DoNotAlterChangeDataCaptureObjects = (布林值 ' True')|如果為 true，則不會改變異動資料擷取物件。|
|**/p:**|DoNotAlterReplicatedObjects = (布林值 ' True')|指定驗證期間是否識別有複寫的物件。|
|**/p:**|DoNotDropObjectType=(STRING)|物件型別時不應捨棄當 DropObjectsNotInSource 為 true。 有效的物件類型名稱為 Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers。 |
|**/p:**|DoNotDropObjectTypes=(STRING)|當 DropObjectsNotInSource 為 true 時不應捨棄的分號分隔物件類型清單。 有效的物件類型名稱為 Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers。|
|**/p:**|DropConstraintsNotInSource = (布林值 ' True')|指定當您發行至資料庫時，是否要從目標資料庫中卸除不存在資料庫快照集 (.dacpac) 檔案中的條件約束。|
|**/p:**|DropDmlTriggersNotInSource = (布林值 ' True')|指定當您發行至資料庫時，是否要從目標資料庫中卸除不存在資料庫快照集 (.dacpac) 檔案中的 DML 觸發程序。|
|**/p:**|DropExtendedPropertiesNotInSource = (布林值 ' True')|指定當您發行至資料庫時，是否要從目標資料庫中卸除不存在資料庫快照集 (.dacpac) 檔案中的擴充屬性。|
|**/p:**|DropIndexesNotInSource = (布林值 ' True')|指定當您發行至資料庫時，是否要從目標資料庫中卸除不存在資料庫快照集 (.dacpac) 檔案中的索引。|
|**/p:**|DropObjectsNotInSource=(BOOLEAN)|指定當您發行至資料庫時，是否要從目標資料庫中卸除不存在資料庫快照集 (.dacpac) 檔案中的物件。 此值的優先順序高過 DropExtendedProperties。|
|**/p:**|DropPermissionsNotInSource=(BOOLEAN)|指定當您發行更新至資料庫時，是否要從目標資料庫中卸除不存在資料庫快照集 (.dacpac) 檔案中的權限。|
|**/p:**|DropRoleMembersNotInSource=(BOOLEAN)|指定當您發行更新至資料庫時，是否要從目標資料庫中卸除資料庫快照集 (.dacpac) 檔案中沒有定義的角色成員。|
|**/p:**|DropStatisticsNotInSource = (布林值 ' True')|指定當您發行至資料庫時，是否要從目標資料庫卸除不存在於資料庫快照集 (.dacpac) 檔案中的統計資料。|
|**/p:**|ExcludeObjectType=(STRING)|部署期間應該忽略的物件類型。 有效的物件類型名稱為 Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers。|
|**/p:**|ExcludeObjectTypes=(STRING)|以分號區隔的物件類型清單，列出部署期間應該忽略的物件類型。 有效的物件類型名稱為 Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers。|
|**/p:**|GenerateSmartDefaults=(BOOLEAN)|在更新含有資料且資料行不允許 null 值的資料表時，自動提供預設值。|
|**/p:**|IgnoreAnsiNulls = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新 ANSI NULLS 設定的差異。|
|**/p:**|IgnoreAuthorizer=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新授權者的差異。|
|**/p:**|IgnoreColumnCollation=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新資料行定序的差異。|
|**/p:**|IgnoreComments=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新註解的差異。|
|**/p:**|IgnoreCryptographicProviderFilePath = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新密碼編譯提供者之檔案路徑的差異。|
|**/p:**|IgnoreDdlTriggerOrder=(BOOLEAN)|指定當您發行至資料庫或伺服器時，應該忽略或更新資料定義語言 (Data Definition Language) (DDL) 觸發程序的順序差異。|
|**/p:**|IgnoreDdlTriggerState=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新資料定義語言 (Data Definition Language) (DDL) 觸發程序之啟用或停用狀態的差異。|
|**/p:**|IgnoreDefaultSchema=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新預設結構描述的差異。 |
|**/p:**|IgnoreDmlTriggerOrder=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新資料操作語言 (DML) 觸發程序的順序差異。| 
|**/p:**|IgnoreDmlTriggerState=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新 DML 觸發程序之啟用或停用狀態的差異。 |
|**/p:**|IgnoreExtendedProperties=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新擴充屬性的差異。 |
|**/p:**|IgnoreFileAndLogFilePath = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新檔案和記錄檔之路徑的差異。 |
|**/p:**|IgnoreFilegroupPlacement = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新 FILEGROUP 中物件位置的差異。| 
|**/p:**|IgnoreFileSize = (布林值 ' True')|指定當您發行至資料庫時，應該忽略檔案大小的差異或應該發出警告。 |
|**/p:**|IgnoreFillFactor = (布林值 ' True')|指定當您發行至資料庫時，應該忽略索引儲存體之填滿因數的差異或應該發出警告|
|**/p:**|IgnoreFullTextCatalogFilePath = (布林值 ' True')|指定當您發行至資料庫時，應該忽略全文檢索目錄之檔案路徑的差異或應該發出警告。| 
|**/p:**|IgnoreIdentitySeed=(BOOLEAN)|指定當您發行更新至資料庫時，應該忽略或更新識別欄位之種子的差異。 |
|**/p:**|IgnoreIncrement=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新識別欄位之增量的差異。 |
|**/p:**|IgnoreIndexOptions=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新索引選項的差異。 |
|**/p:**|IgnoreIndexPadding = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新索引填補的差異。 |
|**/p:**|IgnoreKeywordCasing = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新關鍵字之大小寫的差異。 |
|**/p:**|IgnoreLockHintsOnIndexes=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新索引之鎖定提示的差異。 |
|**/p:**|IgnoreLoginSids = (布林值 ' True')| 指定當您發行至資料庫時，應該忽略或更新安全性識別碼 (SID) 的差異。| 
|**/p:**|IgnoreNotForReplication=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新不可複寫設定。 |
|**/p:**|IgnoreObjectPlacementOnPartitionScheme = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新物件在資料分割配置上的位置。|
 |**/p:**|IgnorePartitionSchemes=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新資料分割配置和函式的差異。|
|**/p:**|IgnorePermissions=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新權限的差異。 |
|**/p:**|IgnoreQuotedIdentifiers = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新引號識別項設定的差異。 |
|**/p:**|IgnoreRoleMembership=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新登入之角色成員資格的差異。 |
|**/p:**|IgnoreRouteLifetime = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新 SQL Server 將路由保留在路由表中之時間長短的差異|
|**/p:**|IgnoreSemicolonBetweenStatements = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新 T-SQL 陳述式間之分號的差異。| 
|**/p:**|IgnoreTableOptions=(BOOLEAN)|指定當您發行至資料庫時，將忽略或更新資料表選項的差異。| 
|**/p:**|IgnoreUserSettingsObjects=(BOOLEAN)|指定當您發行至資料庫時，將忽略或更新使用者設定物件的差異。|
|**/p:**|IgnoreWhitespace = (布林值 ' True')|指定當您發行至資料庫時，將忽略或更新空白字元的差異。 |
|**/p:**|IgnoreWithNocheckOnCheckConstraints=(BOOLEAN)|指定當您發行至資料庫時，將忽略或更新檢查條件約束之 WITH NOCHECK 子句值的差異。| 
|**/p:**|IgnoreWithNocheckOnForeignKeys=(BOOLEAN)|指定當您發行至資料庫時，將忽略或更新外部索引鍵之 WITH NOCHECK 子句值的差異。| 
|**/p:**|IncludeCompositeObjects=(BOOLEAN)|將所有複合項目包含在單一發行作業中。|
|**/p:**|IncludeTransactionalScripts=(BOOLEAN)|指定當您發行至資料庫時，是否應該盡可能使用交易陳述式。|
 |**/p:**|NoAlterStatementsToChangeClrTypes=(BOOLEAN)|指定發行在發現差異時一定要卸除並重新建立組件，而不是發出 ALTER ASSEMBLY 陳述式。 |
|**/p:**|PopulateFilesOnFileGroups = (布林值 ' True')|指定在目標資料庫中建立新 FileGroup 時，是否一併建立新檔案。 |
|**/p:**|RegisterDataTierApplication=(BOOLEAN)|指定結構描述是否向資料庫伺服器註冊。 
|**/p:**|RunDeploymentPlanExecutors=(BOOLEAN)|指定執行其他作業時，是否應該執行 DeploymentPlanExecutor 參與者。|
|**/p:**|ScriptDatabaseCollation=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新資料庫定序的差異。 |
|**/p:**|ScriptDatabaseCompatibility=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新資料庫相容性的差異。 |
|**/p:**|ScriptDatabaseOptions = (布林值 ' True')|指定是否應該在發行動作中設定或更新目標資料庫屬性。 |
|**/p:**|ScriptDeployStateChecks=(BOOLEAN)|指定是否在發行指令碼中產生陳述式，來驗證資料庫名稱和伺服器名稱是否符合資料庫專案中指定的名稱。|
|**/p:**|ScriptFileSize=(BOOLEAN)|控制將檔案加入至檔案群組時是否指定大小。 |
|**/p:**|ScriptNewConstraintValidation = (布林值 ' True')|在發行結束的所有條件約束會驗證當做單一集合，避免檢查或外部索引鍵條件約束在發行導致資料錯誤。 如果設定為 False，您將會發行條件約束而不檢查對應的資料。|
|**/p:**|ScriptRefreshModule = (布林值 ' True')|在發行指令碼的結尾包含重新整理陳述式。|
|**/p:**|儲存體 = ({檔案&#124;記憶體})|指定在建置資料庫模型時，如何儲存項目。 基於效能考量，預設值為 InMemory。 若為非常龐大的資料庫，則需要 File-backed 儲存體。|
|**/p:**|TreatVerificationErrorsAsWarnings=(BOOLEAN)|指定驗證期間發生的錯誤發行是否應視為警告。 系統會先針對產生的部署計畫執行檢查，再針對您的目標資料庫執行計畫。 計畫驗證會偵測出遺漏僅限於目標的物件 (如索引) 這類必須卸除後才能進行變更的問題。 驗證也會偵測因為參考複合專案而存在相依性 (如資料表或檢視)，但卻不存在於目標資料庫中的情況。 您可能選擇這樣做可以取得所有問題，而不需要第一個錯誤時停止發行動作的完整清單。 |
|**/p:**|UnmodifiableObjectWarnings = (布林值 ' True')|指定在無法修改的物件中發現差異時 (例如檔案的檔案大小或檔案路徑不同) 是否應該產生警告。| 
|**/p:**|VerifyCollationCompatibility = (布林值 ' True')|指定是否驗證定序相容性。| 
|**/p:**|VerifyDeployment = (布林值 ' True')|指定是否應該在發行前執行檢查，以便在出現阻止發行成功的問題時停止發行動作。 例如，如果目標資料庫的外部索引鍵不存在資料庫專案中，因而在您發行時造成錯誤，則發行動作可能會停止。 |
  
## <a name="driftreport-parameters"></a>DriftReport 參數  
**SqlPackage.exe** 報表動作會建立自從上次註冊以來已經對註冊資料庫所做變更的 XML 報表。  
  
### <a name="help-for-driftreport-action"></a>DriftReport 動作的說明。

|參數|簡短形式|ReplTest1|描述|
|---|---|---|---|
|**/Action:**|**/a**|DriftReport|指定要執行的動作。 |
|**/OutputPath:**|**/op**|{string}|指定輸出檔案產生位置的檔案路徑。 |
|**/ OverwriteFiles:**|**/of**|{True&#124;False}|指定 sqlpackage.exe 是否應該覆寫現有的檔案。 指定 false 會導致 sqlpackage.exe 在遇到現有的檔案時中止動作。 預設值是 True。 |
|**/Quiet:**|**/q**|{True&#124;False}|指定是否隱藏詳細的意見反應。 預設為 False。|
|**/ TargetConnectionString:**|**/tcs**|{string}|指定目標資料庫的有效 SQL Server/Azure 連接字串。 如果指定此參數，就應該以獨佔方式將它用於所有其他目標參數。 |
|**/TargetDatabaseName:**|**/tdn**|{string}|指定 sqlpackage.exe 動作目標之資料庫名稱的覆寫。 |
|**/ TargetEncryptConnection:**|**/tec**|{True&#124;False}|指定 SQL 加密是否應該用於目標資料庫連線。 |
|**/ TargetPassword:**|**/tp**|{string}|若為 SQL Server 驗證案例，則定義要用來存取目標資料庫的密碼。 |
|**/ TargetServerName:**|**/tsn**|{string}|定義裝載目標資料庫的伺服器名稱。 |
|**/ TargetTimeout:**|**/tt**|{int}|指定建立目標資料庫連線的逾時 (以秒為單位)。 Azure AD 中，建議您使用這個值是大於或等於為 30 秒。|
|**/ TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|指定是否要使用 SSL 來加密目標資料庫連線並且略過驗證信任的憑證鏈結。 |
|**/ TargetUser:**|**/tu**|{string}|若為 SQL Server 驗證案例，則定義要用以存取目標資料庫的 SQL Server 使用者。 |
|**/ TenantId:**|**/tid**|{string}|代表 Azure AD 租用戶識別碼或網域名稱。 此選項，才可支援客體或匯入 Azure AD 使用者，以及 Microsoft 帳戶，例如 outlook.com、 hotmail.com 或 live.com。 如果省略這個參數，則 Azure AD 的預設租用戶識別碼會使用，假設已驗證的使用者是此 ad 原生的使用者。 不過，在此情況下任何客體或匯入的使用者和/或裝載於此 Azure AD 的 Microsoft 帳戶不支援，而且此作業會失敗。 <br/> 如需 Active Directory 通用驗證的詳細資訊，請參閱[通用驗證與 SQL Database 和 SQL 資料倉儲 （SSMS 支援 MFA）](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)。|
|**/ UniversalAuthentication:**|**/ua**|{True&#124;False}|指定是否應該使用通用驗證。 設為 True 時，互動式驗證通訊協定已啟用支援 MFA。 此選項也可以用於 Azure AD 驗證，而不使用互動式要求使用者輸入其使用者名稱和密碼或整合式的驗證 （Windows 認證） 通訊協定的 MFA。 SourceConnectionString 時 /UniversalAuthentication 設為 True 時，可以指定沒有 Azure AD 驗證 (/ scs)。 SourceConnectionString 當 /UniversalAuthentication 設定為 False 時，必須指定 Azure AD 驗證 (/ scs)。 <br/> 如需 Active Directory 通用驗證的詳細資訊，請參閱[通用驗證與 SQL Database 和 SQL 資料倉儲 （SSMS 支援 MFA）](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)。|

## <a name="script-parameters-and-properties"></a>指令碼參數與屬性  
**SqlPackage.exe** 指令碼動作建立的 Transact-SQL 累加更新指令碼會更新目標資料庫的結構描述，使其符合來源資料庫的結構描述。  
  
### <a name="help-for-the-script-action"></a>指令碼動作的說明。
|參數|簡短形式|ReplTest1|描述|
|---|---|---|---|
|**/Action:**|**/a**|指令碼|指定要執行的動作。 |
|**/OutputPath:**|**/op**|{string}|指定輸出檔案產生位置的檔案路徑。 |
|**/ OverwriteFiles:**|**/of**|{True&#124;False}|指定 sqlpackage.exe 是否應該覆寫現有的檔案。 指定 false 會導致 sqlpackage.exe 在遇到現有的檔案時中止動作。 預設值是 True。 |
|**/Profile:**|**/pr**|{string}|指定 DAC 發行設定檔的檔案路徑。 設定檔會定義產生輸出時要使用之屬性及變數的集合。|
|**/Properties:**|**/p**|{PropertyName}={Value}|指定動件特定屬性的名稱/值對：{PropertyName}={Value}。 請參閱特定動作的說明，以便查看該動作的屬性名稱。 範例： sqlpackage.exe /Action： 發行 /？。|
|**/Quiet:**|**/q**|{True&#124;False}|指定是否隱藏詳細的意見反應。 預設為 False。|
|**/ SourceConnectionString:**|**/scs**|{string}|指定來源資料庫的有效 SQL Server/Azure 連接字串。 如果指定此參數，就應該以獨佔方式將它用於所有其他來源參數。 |
|**/SourceDatabaseName:**|**/sdn**|{string}|定義來源資料庫的名稱。 |
|**/ SourceEncryptConnection:**|**/sec**|{True&#124;False}|指定 SQL 加密是否應該用於來源資料庫連線。 |
|**/Sourcefile:**|**/sf**|{string}|指定要當作動作來源使用的來源檔案，而非資料庫。 如果使用此參數，其他來源參數都應該無效。 |
|**/SourcePassword:**|**/sp**|{string}|若為 SQL Server 驗證案例，則定義要用來存取來源資料庫的密碼。 |
|**/ SourceServerName:**|**/ssn**|{string}|定義裝載來源資料庫的伺服器名稱。 |
|**/ SourceTimeout:**|**/st**|{int}|指定建立來源資料庫連線的逾時 (以秒為單位)。 |
|**/ SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|指定是否要使用 SSL 來加密來源資料庫連線並且略過驗證信任的憑證鏈結。 |
|**/SourceUser:**|**/su**|{string}|若為 SQL Server 驗證案例，則定義要用來存取來源資料庫的 SQL Server 使用者。 |
|**/ TargetConnectionString:**|**/tcs**|{string}|指定目標資料庫的有效 SQL Server/Azure 連接字串。 如果指定此參數，就應該以獨佔方式將它用於所有其他目標參數。 |
|**/TargetDatabaseName:**|**/tdn**|{string}|指定 sqlpackage.exe 動作目標之資料庫名稱的覆寫。 |
|**/ TargetEncryptConnection:**|**/tec**|{True&#124;False}|指定 SQL 加密是否應該用於目標資料庫連線。 |
|**/TargetFile:**|**/tf**|{string}| 指定要做為 targetof 動作，而不是資料庫的目標檔案 （亦即.dacpac 檔案）。 如果使用此參數，其他目標參數都應該無效。 這個參數應該是無效的 foractions 僅支援資料庫目標。|
|**/ TargetPassword:**|**/tp**|{string}|若為 SQL Server 驗證案例，則定義要用來存取目標資料庫的密碼。 |
|**/ TargetServerName:**|**/tsn**|{string}|定義裝載目標資料庫的伺服器名稱。 |
|**/ TargetTimeout:**|**/tt**|{int}|指定建立目標資料庫連線的逾時 (以秒為單位)。 Azure AD 中，建議您使用這個值是大於或等於為 30 秒。|
|**/ TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|指定是否要使用 SSL 來加密目標資料庫連線並且略過驗證信任的憑證鏈結。 |
|**/ TargetUser:**|**/tu**|{string}|若為 SQL Server 驗證案例，則定義要用以存取目標資料庫的 SQL Server 使用者。 |
|**/ TenantId:**|**/tid**|{string}|代表 Azure AD 租用戶識別碼或網域名稱。 此選項，才可支援客體或匯入 Azure AD 使用者，以及 Microsoft 帳戶，例如 outlook.com、 hotmail.com 或 live.com。 如果省略這個參數，則 Azure AD 的預設租用戶識別碼會使用，假設已驗證的使用者是此 ad 原生的使用者。 不過，在此情況下任何客體或匯入的使用者和/或裝載於此 Azure AD 的 Microsoft 帳戶不支援，而且此作業會失敗。 <br/> 如需 Active Directory 通用驗證的詳細資訊，請參閱[通用驗證與 SQL Database 和 SQL 資料倉儲 （SSMS 支援 MFA）](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)。|
|**/ UniversalAuthentication:**|**/ua**|{True&#124;False}|指定是否應該使用通用驗證。 設為 True 時，互動式驗證通訊協定已啟用支援 MFA。 此選項也可以用於 Azure AD 驗證，而不使用互動式要求使用者輸入其使用者名稱和密碼或整合式的驗證 （Windows 認證） 通訊協定的 MFA。 SourceConnectionString 時 /UniversalAuthentication 設為 True 時，可以指定沒有 Azure AD 驗證 (/ scs)。 SourceConnectionString 當 /UniversalAuthentication 設定為 False 時，必須指定 Azure AD 驗證 (/ scs)。 <br/> 如需 Active Directory 通用驗證的詳細資訊，請參閱[通用驗證與 SQL Database 和 SQL 資料倉儲 （SSMS 支援 MFA）](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)。|
|**/Variables:**|**/v**|{PropertyName}={Value}|指定動件特定變數的名稱/值對：{VariableName}={Value}。 DACPAC 檔案包含有效 SQLCMD 變數的清單。 如果未針對每一個變數提供值，則將產生錯誤。 |


### <a name="properties-specific-to-the-script-action"></a>指令碼動作特有的屬性：

|屬性|ReplTest1|描述|
|---|---|---|
|**/p:**|AdditionalDeploymentContributorArguments=(STRING)|為部署參與者指定其他部署參與者引數。 這應該是以分號區隔的值清單。
|**/p:**|AdditionalDeploymentContributors=(STRING)|指定部署 dacpac 時應該執行的其他部署參與者。 這應該是以分號區隔的完整組建參與者名稱或識別碼清單。
|**/p:**|AllowDropBlockingAssemblies=(BOOLEAN)|這個屬性是供 SqlClr 部署用來使任何封鎖的組件會在部署計畫中卸除。 根據預設，如果必須卸除任何參考組件，則任何的封鎖/參考組件都會封鎖組件更新。
|**/p:**|AllowIncompatiblePlatform=(BOOLEAN)|指定儘管 SQL Server 平台不相容，是否仍要嘗試動作。
|**/p:**|AllowUnsafeRowLevelSecurityDataMovement=(BOOLEAN)|若此屬性設定為 true，請勿封鎖具有資料列層級安全性之資料表的資料動作。 預設值為 false。
|**/p:**|BackupDatabaseBeforeChanges=(BOOLEAN)|在部署任何變更之前，先備份資料庫。
|**/p:**|BlockOnPossibleDataLoss = (布林值 ' True')|指定如果發行作業可能導致資料遺失，就應該終止發行事件。
|**/p:**|BlockWhenDriftDetected = (布林值 ' True')|指定是否封鎖更新結構描述不再符合註冊或已取消註冊的資料庫。
|**/p:**|CommandTimeout = (INT32 '60')|以秒為單位指定對 SQL Server 執行查詢時的命令逾時。
|**/p:**|CommentOutSetVarDeclarations=(BOOLEAN)|指定在產生的發行指令碼中是否應該將 SETVAR 變數的宣告標記為註解。 如果您計畫在使用 SQLCMD.EXE 等工具進行發行時在命令列指定值，就可以選擇這種做法。
|**/p:**|CompareUsingTargetCollation=(BOOLEAN)|這個設定表示資料庫的定序於部署期間的處理方式；根據預設，如果目標資料庫的定序不符合來源所指定的定序，即會更新目標資料庫的定序。 當設定這個選項時，則應該使用目標資料庫 (或伺服器) 的定序。|
|**/p:**|CreateNewDatabase=(BOOLEAN)|指定當您發行至資料庫時，應該更新目標資料庫或應該卸除並重新建立目標資料庫。
|**/p:**|DatabaseEdition = ({Basic&#124;標準&#124;Premium&#124;預設} 'Default')|定義 Azure SQL Database 的版本。
|**/p:**|DatabaseMaximumSize=(INT32)|定義 Azure SQL Database 的大小上限 (以 GB 表示)。
|**/p:**|DatabaseServiceObjective=(STRING)|定義 Azure SQL Database 的效能等級，例如 "P0" 或 "S1"。
|**/p:**|DeployDatabaseInSingleUserMode=(BOOLEAN)|若為 true，則資料庫會在設定為單一使用者模式後部署。
|**/p:**|DisableAndReenableDdlTriggers = (布林值 ' True')| 指定是否在發行程序開始時停用資料定義語言 (Data Definition Language) (DDL) 觸發程序，並在發行動作結束時重新啟用。|
|**/p:**|DoNotAlterChangeDataCaptureObjects = (布林值 ' True')|如果為 true，則不會改變異動資料擷取物件。
|**/p:**|DoNotAlterReplicatedObjects = (布林值 ' True')|指定驗證期間是否識別已複寫的物件。
|**/p:**|DoNotDropObjectType=(STRING)|物件類型，不應該捨棄當 DropObjectsNotInSource istrue。 有效的物件類型名稱為 Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers。
|**/p:**|DoNotDropObjectTypes=(STRING)|以分號分隔清單的物件類型，不能卸除的 whenDropObjectsNotInSource 為 true。 有效的物件類型名稱為 Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers。
|**/p:**|DropConstraintsNotInSource = (布林值 ' True')|指定當您發行至資料庫時，是否要從目標資料庫中卸除不存在於資料庫快照集 (.dacpac) 檔案中的條件約束。|
|**/p:**|DropDmlTriggersNotInSource = (布林值 ' True')|指定當您發行至資料庫時，是否要從目標資料庫中卸除不存在於資料庫快照集 (.dacpac) 檔案中的 DML 觸發程序。|
|**/p:**|DropExtendedPropertiesNotInSource = (布林值 ' True')|指定當您發行至資料庫時，是否要從目標資料庫中卸除不存在於資料庫快照集 (.dacpac) 檔案中的擴充屬性。|
|**/p:**|DropIndexesNotInSource = (布林值 ' True')|指定當您發行至資料庫時，是否要從目標資料庫中卸除不存在於資料庫快照集 (.dacpac) 檔案中的索引。|
|**/p:**|DropObjectsNotInSource=(BOOLEAN)|指定當您發行至資料庫時，是否要從目標資料庫中卸除不存在於資料庫快照集 (.dacpac) 檔案中的物件。 此值的優先順序高過 DropExtendedProperties。|
|**/p:**|DropPermissionsNotInSource=(BOOLEAN)|指定當您發行更新至資料庫時，是否要從目標資料庫中卸除不存在於資料庫快照集 (.dacpac) 檔案中的權限。|
|**/p:**|DropRoleMembersNotInSource=(BOOLEAN)|指定當您發行更新至資料庫時，是否要從目標資料庫中卸除資料庫快照集 (.dacpac) 檔案中未定義的角色成員。|
|**/p:**|DropStatisticsNotInSource = (布林值 ' True')|指定當您發行至資料庫時，是否要從目標資料庫卸除不存在於資料庫快照集 (.dacpac) 檔案中的統計資料。|
|**/p:**|ExcludeObjectType=(STRING)|部署期間應該忽略的物件類型。 有效物件類型名稱為 Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers。
|**/p:**|ExcludeObjectTypes=(STRING)|以分號區隔的物件類型清單，列出部署期間應該忽略的物件類型。 有效的物件類型名稱為 Aggregates、ApplicationRoles、Assemblies、AsymmetricKeys、BrokerPriorities、Certificates、ColumnEncryptionKeys、ColumnMasterKeys、Contracts、DatabaseRoles、DatabaseTriggers、Defaults、ExtendedProperties、ExternalDataSources、ExternalFileFormats、ExternalTables、Filegroups、FileTables、FullTextCatalogs、FullTextStoplists、MessageTypes、PartitionFunctions、PartitionSchemes、Permissions、Queues、RemoteServiceBindings、RoleMembership、Rules、ScalarValuedFunctions、SearchPropertyLists、SecurityPolicies、Sequences、Services、Signatures、StoredProcedures、SymmetricKeys、Synonyms、Tables、TableValuedFunctions、UserDefinedDataTypes、UserDefinedTableTypes、ClrUserDefinedTypes、Users、Views、XmlSchemaCollections、Audits、Credentials、CryptographicProviders、DatabaseAuditSpecifications、DatabaseScopedCredentials、Endpoints、ErrorMessages、EventNotifications、EventSessions、LinkedServerLogins、LinkedServers、Logins、Routes、ServerAuditSpecifications、ServerRoleMembership、ServerRoles、ServerTriggers。
|**/p:**|GenerateSmartDefaults=(BOOLEAN)|在更新含有資料且資料行不允許 null 值的資料表時，自動提供預設值。
|**/p:**|IgnoreAnsiNulls = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新 ANSI NULLS 設定的差異。
|**/p:**|IgnoreAuthorizer=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新授權者的差異。
|**/p:**|IgnoreColumnCollation=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新資料行定序的差異。
|**/p:**|IgnoreComments=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新註解的差異。
|**/p:**|IgnoreCryptographicProviderFilePath = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新密碼編譯提供者之檔案路徑的差異。
|**/p:**|IgnoreDdlTriggerOrder=(BOOLEAN)|指定當您發行至資料庫或伺服器時，應該忽略或更新資料定義語言 (Data Definition Language) (DDL) 觸發程序的順序差異。|
|**/p:**|IgnoreDdlTriggerState=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新資料定義語言 (Data Definition Language) (DDL) 觸發程序之啟用或停用狀態的差異。|
|**/p:**|IgnoreDefaultSchema=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新預設結構描述的差異。|
|**/p:**|IgnoreDmlTriggerOrder=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新資料操作語言 (DML) 觸發程序的順序差異。|
|**/p:**|IgnoreDmlTriggerState=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新 DML 觸發程序之啟用或停用狀態的差異。|
|**/p:**|IgnoreExtendedProperties=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新擴充屬性的差異。|
|**/p:**|IgnoreFileAndLogFilePath = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新檔案和記錄檔之路徑的差異。|
|**/p:**|IgnoreFilegroupPlacement = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新 FILEGROUP 中物件位置的差異。|
|**/p:**|IgnoreFileSize = (布林值 ' True')|指定當您發行至資料庫時，應該忽略檔案大小的差異或應該發出警告。|
|**/p:**|IgnoreFillFactor = (布林值 ' True')|指定當您發行至資料庫時，應該忽略索引儲存體之填滿因數的差異或應該發出警告。|
|**/p:**|IgnoreFullTextCatalogFilePath = (布林值 ' True')|指定當您發行至資料庫時，是否忽略全文檢索檔案路徑的差異或是否應該發出警告。|
|**/p:**|IgnoreIdentitySeed=(BOOLEAN)|指定當您發行更新至資料庫時，應該忽略或更新識別欄位之種子的差異。|
|**/p:**|IgnoreIncrement=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新識別欄位之增量的差異。|
|**/p:**|IgnoreIndexOptions=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新索引選項的差異。|
|**/p:**|IgnoreIndexPadding = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新索引填補的差異。|
|**/p:**|IgnoreKeywordCasing = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新關鍵字之大小寫的差異。|
|**/p:**|IgnoreLockHintsOnIndexes=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新索引之鎖定提示的差異。|
|**/p:**|IgnoreLoginSids = (布林值 ' True')| 指定當您發行至資料庫時，應該忽略或更新安全性識別碼 (SID) 的差異。|
|**/p:**|IgnoreNotForReplication=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新不可複寫設定。|
|**/p:**|IgnoreObjectPlacementOnPartitionScheme = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新物件在資料分割配置上的位置。|
|**/p:**|IgnorePartitionSchemes=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新資料分割配置和函式的差異。|
|**/p:**|IgnorePermissions=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新權限的差異。|
|**/p:**|IgnoreQuotedIdentifiers = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新引號識別項設定的差異。|
|**/p:**|IgnoreRoleMembership=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新登入之角色成員資格的差異。|
|**/p:**|IgnoreRouteLifetime = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新 SQL Server 將路由保留在路由表中之時間長短的差異。|
|**/p:**|IgnoreSemicolonBetweenStatements = (布林值 ' True')|指定當您發行至資料庫時，應該忽略或更新 T-SQL 陳述式之間的分號差異。|
|**/p:**|IgnoreTableOptions=(BOOLEAN)|指定當您發行至資料庫時，將忽略或更新資料表選項的差異。|
|**/p:**|IgnoreUserSettingsObjects=(BOOLEAN)|指定當您發行至資料庫時，將忽略或更新使用者設定物件的差異。|
|**/p:**|IgnoreWhitespace = (布林值 ' True')|指定當您發行至資料庫時，將忽略或更新空白字元的差異。|
|**/p:**|IgnoreWithNocheckOnCheckConstraints=(BOOLEAN)|指定當您發行至資料庫時，將忽略或更新檢查條件約束之 WITH NOCHECK 子句值的差異。|
|**/p:**|IgnoreWithNocheckOnForeignKeys=(BOOLEAN)|指定當您發行至資料庫時，將忽略或更新外部索引鍵之 WITH NOCHECK 子句值的差異。|
|**/p:**|IncludeCompositeObjects=(BOOLEAN)|將所有複合項目包含在單一發行作業中。|
|**/p:**|IncludeTransactionalScripts=(BOOLEAN)|指定當您發行至資料庫時，是否應該盡可能使用交易陳述式。|
|**/p:**|NoAlterStatementsToChangeClrTypes=(BOOLEAN)|指定發行在發現差異時一定要卸除並重新建立組件，而不是發出 ALTER ASSEMBLY 陳述式。|
|**/p:**|PopulateFilesOnFileGroups = (布林值 ' True')|指定在目標資料庫中建立新 FileGroup 時，是否一併建立新檔案。|
|**/p:**|RegisterDataTierApplication=(BOOLEAN)|指定結構描述是否向資料庫伺服器註冊。|
|**/p:**|RunDeploymentPlanExecutors=(BOOLEAN)|指定執行其他作業時，是否應該執行 DeploymentPlanExecutor 參與者。|
|**/p:**|ScriptDatabaseCollation=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新資料庫定序的差異。|
|**/p:**|ScriptDatabaseCompatibility=(BOOLEAN)|指定當您發行至資料庫時，應該忽略或更新資料庫相容性的差異。|
|**/p:**|ScriptDatabaseOptions = (布林值 ' True')|指定是否應該在發行動作中設定或更新目標資料庫屬性。|
|**/p:**|ScriptDeployStateChecks=(BOOLEAN)|指定是否在發行指令碼中產生陳述式，來驗證資料庫名稱和伺服器名稱是否符合資料庫專案中指定的名稱。|
|**/p:**|ScriptFileSize=(BOOLEAN)|控制將檔案加入至檔案群組時是否指定大小。|
|**/p:**|ScriptNewConstraintValidation = (布林值 ' True')|在發行結束的所有條件約束會驗證當做單一集合，避免檢查或 themiddle 發行的外部索引鍵條件約束導致資料錯誤。 如果設定為 False，您的條件約束會 publishedwithout 檢查對應的資料。|
|**/p:**|ScriptRefreshModule = (布林值 ' True')|在發行指令碼的結尾包含重新整理陳述式。|
|**/p:**|儲存體 = ({檔案&#124;記憶體})|指定在建置資料庫模型時，如何儲存項目。 基於效能考量，預設值為 InMemory。 若為大型資料庫，則需要檔案型儲存體。|
|**/p:**|TreatVerificationErrorsAsWarnings=(BOOLEAN)|指定是否發行期間發生的錯誤驗證應 betreated 為警告。 Generateddeployment 計劃執行檢查，才能針對您的目標資料庫執行計畫。計畫驗證會偵測問題，例如遺失的僅限目標物件 （例如索引），進行變更，必須先卸除。 驗證也會偵測情況下，複合專案中，以參考的相依性 （例如資料表或檢視表） existbecause 但不存在於 thetarget 資料庫。 您可能選擇這樣做可以取得 allissues，而不需要第一個錯誤時停止發行動作的完整清單。|
|**/p:**|UnmodifiableObjectWarnings = (布林值 ' True')|指定在無法修改的物件中發現差異時 (例如檔案的檔案大小或檔案路徑不同) 是否應該產生警告。|
|**/p:**|VerifyCollationCompatibility = (布林值 ' True')|指定是否驗證定序相容性。
|**/p:**|VerifyDeployment = (布林值 ' True')|指定是否應該在發行前執行檢查，以便在出現阻止發行成功的問題時停止發行動作。 例如，如果目標資料庫的外部索引鍵不存在於資料庫專案中，因而在您發行時造成錯誤，則發行動作可能會停止。|
  