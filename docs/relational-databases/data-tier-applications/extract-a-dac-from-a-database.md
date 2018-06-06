---
title: 從資料庫中擷取 DAC | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: data-tier-applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-data-tier-apps
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.extractdacwizard.validationandsummary.f1
- sql13.swb.extractdacwizard.introduction.f1
- sql13.swb.extractdacwizard.selectdatapage.f1
- sql13.swb.extractdacwizard.setdacproperties.f1
- sql13.swb.extractdacwizard.buildandsave.f1
helpviewer_keywords:
- extract DAC
- How to [DAC], extract
- data-tier application [SQL Server], extract
- wizard [DAC], extract
ms.assetid: ae52a723-91c4-43fd-bcc7-f8de1d1f90e5
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f7141252a11e4391d14a4b8aff5240e849ad27d8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="extract-a-dac-from-a-database"></a>從資料庫中擷取 DAC
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  您可以使用 [擷取資料層應用程式精靈] 或 Windows PowerShell 指令碼，從現有的 SQL Server 資料庫中擷取資料層應用程式 (DAC) 封裝。 此擷取程序會建立 DAC 封裝檔案，其中包含資料庫物件及其相關執行個體層級元素的定義。 例如，DAC 封裝檔案會包含資料庫資料表、預存程序、檢視表、使用者以及對應至資料庫使用者的登入。  
  
 
## <a name="before-you-begin"></a>開始之前  
 您可以從位於 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]或 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Service Pack 4 或更新版本之執行個體的資料庫中擷取 DAC。 如果您針對從 DAC 部署的資料庫來執行擷取程序，則只會擷取資料庫中物件的定義。 此程序不會參考 **msdb** 中註冊的 DAC (**中的** master [!INCLUDE[ssSDS](../../includes/sssds-md.md)])。 擷取程序不會在目前的 Database Engine 執行個體中註冊 DAC 定義。 如需有關註冊 DAC 的詳細資訊，請參閱＜ [Register a Database As a DAC](../../relational-databases/data-tier-applications/register-a-database-as-a-dac.md)＞。  
  
##  <a name="LimitationsRestrictions"></a> 限制事項  
 DAC 只能從 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]或 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) 或更新版本的資料庫中進行擷取。 如果 DAC 或包含的使用者中不支援資料庫中的物件，則無法擷取 DAC。 如需有關 DAC 中支援之物件類型的詳細資訊，請參閱＜ [DAC Support For SQL Server Objects and Versions](../../relational-databases/data-tier-applications/dac-support-for-sql-server-objects-and-versions.md)＞。  
  
##  <a name="Permissions"></a> 權限  
 擷取 DAC 至少需要 ALTER ANY LOGIN 和資料庫範圍 VIEW DEFINITION 權限，以及 **sys.sql_expression_dependencies**的 SELECT 權限。 擷取 DAC 可以透過 securityadmin 固定伺服器角色的成員來完成，這個角色的成員也是擷取 DAC 之來源資料庫中 database_owner 固定資料庫角色的成員。 sysadmin 固定伺服器角色的成員或是內建 SQL Server 系統管理員帳戶 **sa** 也可以擷取 DAC。  
  
##  <a name="UsingDACExtractWizard"></a> 使用擷取資料層應用程式精靈  
 **使用精靈擷取 DAC**  
  
1.  在 **[物件總管]** 中，展開含有待擷取 DAC 之資料庫的執行個體的節點。  
  
2.  展開 **[資料庫]** 節點。  
  
3.  以滑鼠右鍵按一下待擷取 DAC 之資料庫的節點，並指向 [工作]，然後選取 [擷取資料層應用程式]。  
  
4.  完成精靈對話方塊：  
  
    1.  [簡介頁面](#Introduction)  
  
    2.  [選取資料頁面](#SelectData)  
  
    3.  [設定屬性頁面](#SetProperties)  
  
    4.  [驗證與摘要頁面](#ValidateSummary)  
  
    5.  [建立封裝頁面](#BuildPackage)  
  
###  <a name="Introduction"></a> 精靈簡介頁面  
 此頁面描述擷取資料層應用程式的步驟。  
  
 **不要再顯示此頁面。** - 按一下此核取方塊，之後就不會再顯示此頁面。  
  
 **下一步 >** - 繼續進行至 [選擇方法] 頁面。  
  
 **取消** ：結束精靈，不從資料庫中擷取資料層應用程式。  
  
 [&#91;擷取精靈&#93;](#UsingDACExtractWizard)  
  
###  <a name="SelectData"></a> Select data page  
選取您想要包含在資料層應用程式 (DAC) 封裝檔案中的參考資料。 在您的 DAC 封裝檔案中包含資料是選擇性的。 DAC 封裝已包含所有受支援資料庫物件和資料庫相關執行個體物件的結構描述。  
  
 您可以在 DAC 封裝檔案中最多包含 10 MB 的參考資料。 不過，若要在 DAC 包含資料表，資料表不可以包含二進位大型物件 (BLOB) 資料類型，例如 **image** 或 **varchar(max)**。 若要擷取大量資料以傳送至另一個資料庫，請使用 SQL Server Integration Services、大量複製公用程式或許多其他資料移轉技術。  
  
 **資料庫資料表** ：選取資料庫資料表旁邊的核取方塊，這些資料庫資料表包含您要併入 DAC 封裝中的資料。 您最多可以選取十個不超過 10,000 資料列的資料表。  
  
 [&#91;擷取精靈&#93;](#UsingDACExtractWizard)  
  
###  <a name="SetProperties"></a> Set properties page  
 您可以使用此精靈的這個頁面來描述資料層應用程式 (DAC)。 這些屬性會用來識別 DAC，並協助您區別其他項目。  
  
 **名稱** ：此名稱會識別 DAC。 它可能與 DAC 封裝檔案的名稱不同，而且應該會描述您的應用程式。 例如，如果此資料庫用於財務應用程式，您可能會想要命名為 DAC Finance。  
  
 **版本 (使用 xx.xx.xx.xx，其中 x 是數字)** ：識別 DAC 版本的數值。 DAC 版本會用於 Visual Studio 中，以便識別開發人員正在處理的 DAC 版本。 部署 DAC 時，此版本會儲存在 **msdb** 資料庫中，而且您之後可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 的 [資料層應用程式] 節點底下檢視此版本。  
  
 **描述**：選擇性。 描述此 DAC。 部署 DAC 時，此描述會儲存在 **msdb** 資料庫中，而且您之後可以在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 的 [資料層應用程式] 節點底下檢視此描述。  
  
 **儲存至 DAC 封裝檔案 (檔案名稱包含 .dacpac 副檔名)**：將 DAC 儲存至副檔名為 .dacpac 的 DAC 封裝檔案。 按一下 **[瀏覽]** 按鈕，即可指定檔案的名稱和位置。  
  
 **覆寫現有檔案** ：如果已經有同名的 DAC 封裝檔案，請選取此核取方塊來取代該檔案。  
  
###  <a name="ValidateSummary"></a> Validation and summary page  
 在這個頁面上，此精靈會驗證資料層應用程式 (DAC) 是否支援所有資料庫物件。 此外，它也會檢查資料庫物件之間的相依性，以便判斷可成功包含在 DAC 中的物件集合。 之後，它會顯示驗證報表並摘要列出您在這個精靈中所選取的選項。 若要變更選項，請按 **[上一步]**。 若要開始擷取 DAC，請按 **[下一步]**。  
  
> **注意！**如果 DAC 不支援一個或多個物件，[下一步] 按鈕就會停用，而且擷取程序便無法繼續。 在這種情況下，建議您移除不支援的物件，然後再次執行此精靈。  
  
 **摘要**：所選取的選項摘要會列在 [DAC 屬性] 底下。 驗證的結果則列在 **[DAC 物件]** 底下。 驗證的結果有三種類型：  
  
-   **物件成功包含在 DAC 中**：表示這些物件及其相依性受到支援，而且可以成功包含在 DAC 中。  
  
-   **物件包含在 DAC 中，但是出現警告**：表示雖然這些物件受到支援，不過卻相依於 DAC 不支援的其他物件。  
  
-   **物件未包含在 DAC 中**：表示這些物件不受到支援，而且必須從資料庫中移除它們，然後才能成功擷取 DAC。  
  
 驗證程序會檢查多個相依性層級。 例如，如果某個預存程序相依於使用不支援之 CLR 資料類型的資料表，此預存程序就會列在 **[物件包含在 DAC 中，但是出現警告]** 底下。  
  
 如果 DAC 不支援一個或多個物件， **[下一步]** 按鈕就會停用，而且擷取程序將無法繼續。 在這種情況下，建議您移除不支援的物件，然後再次執行此精靈。  
  
 **儲存報表**：可讓您儲存以 HTML 為基礎的檔案，其中列出摘要之 [DAC 物件] 節點底下的所有物件。 當 DAC 不支援部分資料庫物件時，這份報表可能會很有用。 您可以先使用此報表來變更或移除不支援的物件，然後再次嘗試擷取 DAC。  
  
 ###  <a name="BuildPackage"></a> Build package page  
 您可以使用這個頁面來監視此精靈擷取資料層應用程式 (DAC) 的進度。  
  
 **動作**：在 [建立並儲存 DAC 封裝檔案] 動作期間，此精靈會從 SQL Server 資料庫中擷取 DAC。 然後，它會在記憶體中建立 DAC 封裝並儲存至您所指定的位置。 若要查看對應步驟的結果，請按一下 **[結果]** 欄中的連結。  
  
 **儲存報表** ：按一下即可將精靈進度的結果儲存至檔案。  
  
 **完成** ：在處理完成之後或是發生錯誤時，按一下即可關閉精靈。  
   
##  <a name="ExtractDACPowerShell"></a> 使用 PowerShell 擷取 DAC  
 **在 PowerShell 指令碼中使用 Extract() 方法，從資料庫中擷取 DAC**  
  
1.  建立 SMO Server 物件，並將它設為含有待擷取 DAC 之資料庫的執行個體。  
  
2.  加入可指定資料庫名稱的變數。  
  
3.  指定 DAC 的中繼資料，例如 DAC 名稱、版本及描述。  
  
4.  為已擷取的 DAC 封裝檔案指定路徑和檔案名稱。  
  
5.  使用上述指定的資訊執行擷取方法。  
  
### <a name="example-powershell"></a>範例 (PowerShell)  
 下列範例會從 MyDB 資料庫中擷取名為 MyApplication 的 DAC。  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Specify the database to extract to a DAC.  
$dbname = "MyDB"  
  
## Specify the DAC metadata.  
$applicationname = "MyApplication"  
$version = "1.0.0.0"  
$description = "This DAC defines the database used by my application."  
  
## Specify the location and name for the extracted DAC package.  
$dacpacPath = "C:\MyDACs\MyApplication.dacpac"  
  
## Extract the DAC.  
$extractionunit = New-Object Microsoft.SqlServer.Management.Dac.DacExtractionUnit($srv, $dbname, $applicationname, $version)  
$extractionunit.Description = $description  
$extractionunit.Extract($dacpacPath)  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料層應用程式](../../relational-databases/data-tier-applications/data-tier-applications.md)  
  
  
