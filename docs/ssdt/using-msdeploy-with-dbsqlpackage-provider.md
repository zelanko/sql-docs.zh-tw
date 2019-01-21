---
title: 搭配 dbSqlPackage 提供者使用 MSDeploy | Microsoft Docs
ms.custom:
- SSDT
ms.date: 04/26/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 213b91ab-03e9-431a-80f0-17eed8335abe
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 128e1feeb3b344a21dbb682d4d41d402060ab1ff
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/14/2019
ms.locfileid: "54256943"
---
# <a name="using-msdeploy-with-dbsqlpackage-provider"></a>搭配 dbSqlPackage 提供者使用 MSDeploy
**DbSqlPackage** 是一種 **MSDeploy** 提供者，可讓您與 SQL Server/SQL Azure 資料庫進行互動。 **DbSqlPackage** 支援下列動作：  
  
-   **Extract**：從即時 SQL Server 或 SQL Azure 資料庫建立資料庫快照集 (.dacpac) 檔案。  
  
-   **Publish**：以累加方式更新資料庫結構描述，以符合來源 .dacpac 檔案的結構描述。  
  
-   **DeployReport**：建立發行動作所做變更的 XML 報表。  
  
-   **Script**：建立相當於「發行動作」所執行指令碼的 Transact\-SQL 指令碼。  
  
如需有關 DACFx 的詳細資訊，請參閱 DACFx Managed API 文件，網址為：[https://msdn.microsoft.com/library/microsoft.sqlserver.dac.aspx](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.aspx) \(機器翻譯\) 或 [SqlPackage.exe](../tools/sqlpackage.md) (DACFx 命令列工具)。  
  
> [!IMPORTANT]  
> dbSqlPackage 提供者功能將從 Visual Studio 的下一個主要版本中移除。 如需如何利用 Web Deploy 進行資料庫發行的相關資訊，請參閱[用於累加資料庫發行的 dbDacFx 提供者](https://www.iis.net/learn/publish/using-web-deploy/dbdacfx-provider-for-incremental-database-publishing) \(英文\)。  
  
## <a name="command-line-syntax"></a>命令列語法  
**MSDeploy** 搭配 **dbSqlPackage** 提供者會使用下列形式的命令列：  
  
```  
  
MSDeploy -verb: MSDeploy-verb -source:dbSqlPackage="Input"[,dbSqlPackage-source-parameters] -dest:dpSqlPackage="Input"[,dbSqlPackage-target-parameters]  
```  
  
## <a name="ms-deploy-verbs"></a>MS-Deploy 動詞命令  
透過在 MS-Deploy 命令列上使用 **-verb** 參數，指定 MS-Deploy 動詞命令。 **dbSqlPackage** 提供者支援下列 **MSDeploy** 動詞命令：  
  
|動詞命令|Description|  
|--------|---------------|  
|dump|提供有關 .dacpac 檔案中所含來源資料庫的資訊，包括名稱、版本號碼和描述。 在命令列上使用下列格式來指定來源資料庫：<br /><br />**msdeploy -verb:dump -source:dbSqlPackage="**_.dacpac-file-path_**"**|  
|sync|在命令列上使用下列格式來指定 dbSqlPackage 動作：<br /><br />**msdeploy -verb:sync -source:dbSqlPackage**="input" _[,DbSqlPackage-source-parameters] -_**dest:dbSqlPackage**="input" *[,DbSqlPackage-destination-parameters]*<br /><br />請參閱下列各節以了解 sync 動詞命令的有效來源和目的參數。|  
  
## <a name="dbsqlpackage-source"></a>dbSqlPackage 來源  
**dbSqlPackage** 提供者可接受的輸入包括有效的 SQL Server/SQL Azure 連接字串，或是磁碟上 .dacpac 檔案的路徑。  針對提供者指定輸入來源的語法如下：  
  
|輸入|預設|Description|  
|---------|-----------|---------------|  
|**-source:dbSqlPackage=**{*input*}|**N/A**|*input* 是有效的 SQL Server 或 SQL Azure 連接字串，或是磁碟上 .dacpac 檔案的路徑。<br /><br />**注意：** 使用連接字串作為輸入來源時，支援的連接字串屬性只有 *InitialCatalog、DataSource、UserID、Password、IntegratedSecurity、Encrypt、TrustServerCertificate* 和 *ConnectionTimeout*。|  
  
如果您的輸入來源是即時 SQL Server/SQL Azure 資料庫的連接字串，**dbSqlPackage** 將會從即時 SQL Server/SQL Azure 資料庫中擷取資料庫快照集 (.dacpac 格式的檔案)。  
  
**來源**參數包括：  
  
|參數|預設|Description|  
|-------------|-----------|---------------|  
|**Profile**:{ *string*}|不適用|指定 DAC 發行設定檔的檔案路徑。 設定檔會定義產生結果 dacpac 時要使用之屬性及變數的集合。 發行設定檔會傳遞給目的地，並且在執行 **Publish**、**Script** 或 **DeployReport** 動作時當作預設選項使用。|  
|**DacApplicationName**={ *string* }|資料庫名稱|定義要儲存在 DACPAC 中繼資料中的應用程式名稱。 預設字串為資料庫名稱。|  
|**DacMajorVersion** ={*integer*}|**1**|定義要儲存在 DACPAC 中繼資料中的主要版本。|  
|**DacMinorVersion**={*integer*}|**0**|定義要儲存在 DACPAC 中繼資料中的次要版本。|  
|**DacApplicationDescription**={ *string* }|不適用|定義要儲存在 DACPAC 中繼資料中的應用程式描述。|  
|**ExtractApplicationScopedObjectsOnly={True &#124; False}**|**True**|如果為 **True**，只會從來源擷取應用程式範圍的物件。 如果為 **False**，則會擷取應用程式範圍的物件和非應用程式範圍的物件。|  
|**ExtractReferencedServerScopedElements={True &#124; False}**|**True**|若為 **True**，則擷取來源資料庫物件所參考的登入、伺服器稽核及認證物件。|  
|**ExtractIgnorePermissions={True &#124; False}**|**False**|如果為 **True**，則忽略擷取所有擷取物件的權限。如果為 **False**，則不忽略。|  
|**ExtractStorage={File&#124;Memory}**|**檔案**|指定支援儲存體的類型，以供結構描述模型在擷取期間使用。|  
|**ExtractIgnoreExtendedProperties={True&#124;False}**|**False**|指定是否應該忽略擴充屬性。|  
|**VerifyExtraction = {True&#124;False}**|**False**|指定是否應該驗證擷取的 dacpac。|  
  
## <a name="dbsqlpackage-destination"></a>DbSqlPackage 目的地  
**dbSqlPackage** 提供者可接受有效的 SQL Server/SQL Azure 連接字串或磁碟上 .dacpac 檔案的路徑做為目的輸入。  針對提供者指定目的地的語法如下：  
  
|輸入|預設|Description|  
|---------|-----------|---------------|  
|-**dest:dbSqlPackage**={*input*}|不適用|*input* 是有效的 SQL Server 或 SQL Azure 連接字串，或是磁碟上 .dacpac 檔案的完整或部分路徑。 如果 *input* 是檔案路徑，就不得指定其他參數。|  
  
下列的**目的地**參數可供所有 **dbSqlPackage** 作業使用：  
  
|屬性|預設|Description|  
|------------|-----------|---------------|  
|**Action={Publish&#124;DeployReport&#124;Script}**|不適用|指定要在**目的地**執行之動作的選擇性參數。|  
|**AllowDropBlockingAssemblies ={True &#124; False}**|**False**|指定 **SqlClr** 發行是否會在部署計畫中卸除封鎖的組件。 根據預設，如果必須卸除任何參考組件，則該封鎖或參考組件會封鎖組件更新。|  
|**AllowIncompatiblePlatform={True &#124; False}**|**False**|指定儘管 SQL Server 平台可能不相容，是否仍要進行發行動作。|  
|**BackupDatabaseBeforeChanges={True &#124; False}**|**False**|在部署任何變更之前，先備份資料庫。|  
|**BlockOnPossibleDataLoss={ True &#124; False}**|**True**|指定如果發行作業可能導致資料遺失時，是否會終止發行事件。|  
|**BlockWhenDriftDetected={ True &#124; False}**|**True**|指定是否封鎖更新結構描述不再符合註冊或已取消註冊的資料庫。|  
|**CommentOutSetVarDeclarations= {True &#124; False}**|**False**|指定在產生的發行指令碼中 **SETVAR** 變數宣告是否標記為註解。 如果您打算在發行時使用 **SQLCMD.exe** 等工具從命令列指定值，就可以選擇這種做法。|  
|**CompareUsingTargetCollation={ True &#124; False}**|**False**|這個設定表示資料庫的定序於部署期間的處理方式。如果目標資料庫的定序不符合來源所指定的定序，預設會更新目標資料庫的定序。  當設定這個選項時，則應該使用目標資料庫 (或伺服器) 的定序。|  
|**CreateNewDatabase={ True &#124; False}**|**False**|指定當您發行至資料庫時，應該更新目標資料庫或應該卸除並重新建立目標資料庫。|  
|**DeployDatabaseInSingleUserMode={ True &#124; False}**|**False**|若為 **True**，則資料庫會在設定為單一使用者模式後部署。|  
|**DisableAndReenableDdlTriggers={True &#124; False}**|**True**|指定是否在發行程序開始時停用資料定義語言 (DDL) 觸發程序，並在發行動作結束時重新啟用。|  
|**DoNotAlterChangeDataCaptureObjects={ True &#124; False}**|**True**|如果為 **True**，則不會改變異動資料擷取物件。|  
|**DoNotAlterReplicatedObjects=( True &#124; False}**|**True**|指定驗證期間是否識別有複寫的物件。|  
|**DropConstraintsNotInSource= {True &#124; False}**|**True**|指定當您發行至資料庫時，發行動作是否要從目標資料庫中卸除不存在資料庫快照集 (.dacpac) 中的條件約束。|  
|**DropDmlTriggersNotInSource= {True &#124; False}**|**True**|指定當您發行至資料庫時，發行動作是否要從目標資料庫中卸除不存在資料庫快照集 (.dacpac) 中的資料操作語言 (DML) 觸發程序。|  
|**DropExtendedPropertiesNotInSource= {True &#124; False}**|**True**|指定當您發行至資料庫時，發行動作是否要從目標資料庫中卸除不存在資料庫快照集 (.dacpac) 中的擴充屬性。|  
|**DropIndexesNotInSource= {True &#124; False}**|**True**|指定當您發行至資料庫時，發行動作是否要從目標資料庫中卸除不存在資料庫快照集 (.dacpac) 中的索引。|  
|**DropObjectsNotInSource= {True &#124; False}**|**False**|指定當您發行至資料庫時，是否要從目標資料庫中卸除不存在資料庫快照集 (.dacpac) 檔案中的物件。|  
|**DropPermissionsNotInSource= {True &#124; False}**|**False**|指定當您發行至資料庫時，發行動作是否要從目標資料庫中卸除不存在資料庫快照集 (.dacpac) 中的權限。|  
|**DropRoleMembersNotInSource= {True &#124; False}**|**False**|指定當您發行至資料庫時，發行動作是否要從目標資料庫中卸除不存在資料庫快照集 (.dacpac) 中的角色成員。|  
|**GenerateSmartDefaults={True &#124; False}**|**False**|指定 **SqlPackage.exe** 是否會在更新含有資料且資料行不允許 Null 值的資料表時自動提供預設值。|  
|**IgnoreAnsiNulls= {True &#124; False}**|**False**|指定當您發行至資料庫時，應該忽略或更新 **ANSI NULLS** 設定的差異。|  
|**IgnoreAuthorizer= {True &#124; False}**|**False**|指定當您發行至資料庫時，應該忽略或更新授權者的差異。|  
|**IgnoreColumnCollation= {True &#124; False}**|**False**|指定當您發行至資料庫時，應該忽略或更新資料行定序的差異。|  
|**IgnoreComments= {True &#124; False}**|**False**|指定當您發行至資料庫時，應該忽略或更新註解順序的差異。|  
|**IgnoreCryptographicProviderFile= {True &#124; False}**|**True**|指定當您發行至資料庫時，應該忽略或更新密碼編譯提供者檔案路徑的差異。|  
|**IgnoreDdlTriggerOrder= {True &#124; False}**|**False**|指定當您發行至資料庫時，應該忽略或更新資料定義語言 (DDL) 觸發程序順序的差異。|  
|**IgnoreDdlTriggerState={True &#124; False}**|**False**|指定當您發行至資料庫時，應該忽略或更新 DDL 觸發程序之啟用或停用狀態的差異。|  
|**IgnoreDefaultSchema={True &#124; False}**|**False**|指定當您發行至資料庫時，應該忽略或更新預設結構描述的差異。|  
|**IgnoreDmlTriggerOrder= {True &#124; False}**|**False**|指定當您發行至資料庫時，應該忽略或更新 DML 觸發程序順序的差異。|  
|**IgnoreDmlTriggerState= {True &#124; False}**|**False**|指定當您發行至資料庫時，應該忽略或更新 DML 觸發程序之啟用或停用狀態的差異。|  
|**IgnoreExtendedProperties= {True &#124; False}**|**False**|指定當您發行至資料庫時，應該忽略或更新擴充屬性的差異。|  
|**IgnoreFileAndLogFilePath={True &#124; False}**|**True**|指定當您發行至資料庫時，應該忽略或更新檔案和記錄檔之路徑的差異。|  
|**IgnoreFilegroupPlacement= {True &#124; False}**|**True**|指定當您發行至資料庫時，應該忽略或更新 **FILEGROUP** 所在位置的差異。|  
|**IgnoreFileSize= {True &#124; False}**|**True**|指定當您發行至資料庫時，應該忽略或更新檔案大小的差異。|  
|**IgnoreFillFactor= {True &#124; False}**|**True**|指定當您發行至資料庫時，應該忽略或更新填滿因數的差異。|  
  
|屬性|預設|Description|  
|------------|-----------|---------------|  
|**IgnoreFullTextCatalogFilePath= {True &#124; False}**|**True**|指定當您發行至資料庫時，應該忽略或更新全文檢索索引檔案之路徑的差異。|  
|**IgnoreIdentitySeed= {True &#124; False}**|**False**|指定當您發行至資料庫時，應該忽略或更新識別欄位之種子的差異。|  
|**IgnoreIncrement= {True &#124; False}**|**False**|指定當您發行至資料庫時，應該忽略或更新識別欄位之增量的差異。|  
|**IgnoreIndexOptions ={True &#124; False}**|**False**|指定當您發行至資料庫時，應該忽略或更新索引選項的差異。|  
|**IgnoreIndexPadding= {True &#124; False}**|**True**|指定當您發行至資料庫時，應該忽略或更新索引填補的差異。|  
|**IgnoreKeywordCasing= {True &#124; False}**|**True**|指定當您發行至資料庫時，應該忽略或更新關鍵字大小寫的差異。|  
|**IgnoreLockHintsOnIndexes= {True &#124; False}**|**False**|指定當您發行至資料庫時，應該忽略或更新索引之鎖定提示的差異。|  
|**IgnoreLoginSids= {True &#124; False}**|**True**|指定當您發行至資料庫時，應該忽略或更新安全性識別碼 (SID) 的差異。|  
|**IgnoreNotForReplication= {True &#124; False}**|**False**|指定當您發行至資料庫時，應該忽略或更新不可複寫設定。|  
|**IgnoreObjectPlacementOnPartitionScheme= {True &#124; False}**|**True**|指定當您發行至資料庫時，應該忽略或更新物件在資料分割區配置上的位置。|  
|**IgnorePartitionSchemes= {True &#124; False}**|**False**|指定當您發行至資料庫時，應該忽略或更新資料分割配置和函數的差異。|  
|**IgnorePermissions= {True &#124; False}**|**False**|指定當您發行至資料庫時，應該忽略或更新權限的差異。|  
|**IgnoreQuotedIdentifiers= {True &#124; False}**|**False**|指定當您發行至資料庫時，應該忽略或更新引號識別項設定的差異。|  
|**IgnoreRoleMembership={True &#124; False}**|**False**|指定當您發行至資料庫時，應該忽略或更新登入之角色成員資格的差異。|  
|**IgnoreRouteLifetime= {True &#124; False}**|**True**|指定當您發行至資料庫時，應該忽略或更新登入之角色成員資格的差異。|  
|**IgnoreSemicolonBetweenState= {True &#124; False}**|**True**|指定當您發行至資料庫時，應該忽略或更新 Transact-SQL 陳述式之間的分號差異。|  
|**IgnoreTableOptions= {True &#124; False}**|**False**|指定當您發行至資料庫時，應該忽略或更新資料表選項的差異。|  
|**IgnoreUserSettingsObjects= {True &#124; False}**|**False**|指定當您發行至資料庫時，應該忽略或更新使用者設定選項的差異。|  
|**IgnoreWhitespace= {True &#124; False}**|**True**|指定當您發行至資料庫時，應該忽略或更新空白字元的差異。|  
|**IgnoreWithNocheckOnCheckConstraints={True &#124; False}**|**False**|指定當您發行至資料庫時，應該忽略或更新檢查條件約束之 **WITH NOCHECK** 子句值的差異。|  
|**IgnoreWithNocheckOnForeignKeys={True &#124; False}**|**False**|指定當您發行至資料庫時，應該忽略或更新外部索引鍵之 **WITH NOCHECK** 子句值的差異。|  
|**IncludeCompositeObjects= {True &#124; False}**|**False**|指定是否將所有複合項目包含在單一發行作業中。|  
|**IncludeTransactionalScripts={True &#124; False}**|**False**|指定當您發行至資料庫時，是否應該盡可能使用交易陳述式。|  
|**NoAlterStatementsToChangeClrTypes={True &#124; False}**|**False**|指定發行在發現差異時一定要卸除並重新建立組件，而不是發出 ALTER ASSEMBLY 陳述式。|  
|**PopulateFilesOnFilegroups= {True &#124; False}**|**True**|指定在目標資料庫中建立新 **FileGroup** 時，是否一併建立新檔案。|  
|**RegisterDataTierApplication={True &#124; False}**|**False**|指定結構描述是否向資料庫伺服器註冊。|  
|**ScriptDatabaseCollation {True &#124; False}**|**False**|指定當您發行至資料庫時，應該忽略或更新資料庫定序的差異。|  
|**ScriptDatabaseCompatibility= {True &#124; False}**|**True**|指定當您發行至資料庫時，應該忽略或更新資料庫相容性的差異。|  
|**ScriptDatabaseOptions= {True &#124; False}**|**True**|指定當您發行至資料庫時，應該設定或更新目標資料庫屬性。|  
|**ScriptFileSize={True &#124; False}**|**False**|控制將檔案加入至檔案群組時是否指定大小。|  
|**ScriptNewConstraintValidation= {True &#124; False}**|**True**|指定是否在發行結束時，將所有條件約束當做單一集合進行驗證，避免檢查或外部索引鍵條件約束在發行動作進行中導致資料錯誤。 如果這個選項是 **False**，便會發行條件約束而不檢查對應的資料。|  
|**ScriptDeployStateChecks={True &#124; False}**|**False**|指定是否在發行指令碼中產生陳述式，來驗證資料庫名稱和伺服器名稱是否符合資料庫專案中指定的名稱。|  
|**ScriptRefreshModule= {True &#124; False}**|**True**|指定是否在發行指令碼的結尾包含重新整理陳述式。|  
|**Storage={File&#124;Memory}**|**記憶體**|指定在建置資料庫模型時，如何儲存項目。 基於效能考量，預設值為 **Memory**。 若為非常龐大的資料庫，則需要 File-backed 儲存體。|  
|**TreatVerificationErrorsAsWarnings= {True &#124; False}**|**False**|指定是否將發行驗證期間所發生的錯誤視為警告。 系統會先針對產生的部署計畫執行檢查，之後再針對目標資料庫執行計畫。 計畫驗證會偵測出遺漏僅限於目標的物件 (例如索引) 這類必須卸除後才能進行變更的問題。 驗證也會偵測因為參考複合專案而有相依性 (例如資料表或檢視) 存在，但是卻不存在目標資料庫中的情況。 您可以選擇將驗證錯誤視為警告，以取得所有問題的清單，而不讓發行動作在第一次錯誤時就停止。|  
|**UnmodifiableObjectWarnings= {True &#124; False}**|**True**|指定在無法修改的物件中發現差異時 (例如檔案的檔案大小或檔案路徑不同) 是否產生警告。|  
|**VerifyCollationCompatibility={True &#124; False}**|**True**|指定是否驗證定序相容性。|  
|**VerifyDeployment={True &#124; False}**|**True**|指定是否在發行前執行檢查，以便在出現阻止發行成功的問題時停止發行動作。 例如，如果因為目標資料庫的外部索引鍵不存在資料庫專案中，而在發行期間成錯誤，則您的發行動作就可能會停止。|  
  
> [!NOTE]  
> 任何指定的目的參數都將覆寫來源發行設定檔中指定的參數。  
  
> [!NOTE]  
> 您必須在發行設定檔來源參數中指定 **SQLCMD** 變數和值，因為它們無法指定為目的地參數。  
  
下列的**目的地**參數只提供 **DeployReport** 和 **Script** 作業使用：  
  
|參數|預設|Description|  
|-------------|-----------|---------------|  
|**OutputPath**={ *string* }|不適用|選擇性參數，告知 **dbSqlPackage** 在 *string* 所指定的磁碟位置建立 DeployReport XML 輸出檔或 Script SQL 輸出檔。 這個動作會覆寫目前在 string 所指定位置上的任何指令碼。|  
  
> [!NOTE]  
> 如果沒有針對 **DeployReport** 或**Script** 動作提供 **OutputPath** 參數，就會以訊息的形式傳回輸出。  
  
## <a name="examples"></a>範例  
下面是使用 **dbSqlPackage** 之 **Extract** 作業的範例語法：  
  
```  
MSDeploy.exe -verb:sync -source:dbSqlPackage="<source connection string>",<source parameter> -dest:dbSqlPackage="<target dacpac file path>"  
```  
  
下面是使用 **dbSqlPackage** 之 **Publish** 作業的範例語法：  
  
```  
MSDeploy.exe -verb:sync -source:dbSqlPackage="<source dacpac file path>" -dest:dbSqlPackage="<target SQL Server/SQL Azure connection string>",Action=Publish,<destination parameters>  
```  
  
下面是使用 **dbSqlPackage** 之 **DeployReport** 作業的範例語法：  
  
```  
MSDeploy.exe -verb:sync -source:dbSqlPackage="<source dacpac file path>" -dest:dbSqlPackage="<target SQL Server/SQL Azure connection string>",Action=DeployReport,OutputPath="<path to output XML file>",<destination parameters>  
```  
  
下面是使用 **dbSqlPackage** 之 **Script** 作業的範例語法：  
  
```  
MSDeploy.exe -verb:sync -source:dbSqlPackage="<source dacpac file path>" -dest:dbSqlPackage="<target SQL Server/SQL Azure connection string>",Action=Script,OutputPath="<path to output sql script>",<destination parameters>  
```  
  
