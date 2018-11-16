---
title: 將資料庫註冊為 DAC | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.registerdacwizard.registerdac.f1
- sql12.swb.registerdacwizard.summary.f1
- sql12.swb.registerdacwizard.introduction.f1
- sql12.swb.registerdacwizard.setproperties.f1
helpviewer_keywords:
- wizard [DAC], register
- How to [DAC], register
- register DAC
- data-tier application [SQL Server], register
ms.assetid: 08e52aa6-12f3-41dd-a793-14b99a083fd5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c5bf53045abe0f93e2ff1e07ec17d31f7d58248b
ms.sourcegitcommit: 9ece10c2970a4f0812647149d3de2c6b75713e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/16/2018
ms.locfileid: "51814071"
---
# <a name="register-a-database-as-a-dac"></a>將資料庫註冊為 DAC
  使用任何一種**註冊資料層應用程式精靈**或 Windows PowerShell 指令碼來建立資料層應用程式 (DAC) 定義，以便描述現有的資料庫中的物件，並註冊 DAC 定義中的`msdb`系統資料庫 (**主要**在[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)])。  
  
-   **Before you begin:**  [Limitations and Restrictions](#LimitationsRestrictions), [Permissions](#Permissions)  
  
-   **使用下列項目，升級 DAC**  [註冊資料層應用程式精靈](#UsingRegisterDACWizard)、 [PowerShell](#RegisterDACPowerShell)  
  
## <a name="before-you-begin"></a>開始之前  
 註冊程序會建立 DAC 定義，以定義資料庫中的物件。 DAC 定義和資料庫的組合會形成 DAC 執行個體。 如果將資料庫註冊為 Database Engine 之受管理的執行個體上的 DAC，下次從執行個體將公用程式收集組傳送到公用程式控制點時，註冊的 DAC 將會合併到 SQL Server 公用程式中。 然後 DAC 會出現在  [公用程式總管] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **[部署的資料層應用程式]** 節點中，並在  詳細資料頁面中報告。  
  
###  <a name="LimitationsRestrictions"></a> 限制事項  
 DAC 註冊只能在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]或 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) 或更新版本的資料庫上執行。 如果已經針對資料庫註冊 DAC，將無法執行 DAC 註冊。 例如，如果資料庫是藉由部署 DAC 所建立，您將無法執行 [註冊資料層應用程式精靈]。  
  
 如果 DAC 或包含的使用者中不支援資料庫中的物件，則無法註冊 DAC。 如需有關 DAC 中支援之物件類型的詳細資訊，請參閱＜ [DAC Support For SQL Server Objects and Versions](dac-support-for-sql-server-objects-and-versions.md)＞。  
  
###  <a name="Permissions"></a> 權限  
 在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體中註冊 DAC 至少需要 ALTER ANY LOGIN 和資料庫範圍 VIEW DEFINITION 權限、 **sys.sql_expression_dependencies**的 SELECT 權限，以及 **dbcreator** 固定伺服器角色的成員資格。 **系統管理員** 固定伺服器角色的成員或是內建 SQL Server 系統管理員帳戶 **sa** 也可以註冊 DAC。 在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 中註冊不包含登入的 DAC，需要 **dbmanager** 或 **serveradmin** 角色的成員資格。 在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 中註冊包含登入的 DAC，需要 **loginmanager** 或 **serveradmin** 角色的成員資格。  
  
##  <a name="UsingRegisterDACWizard"></a> 使用註冊資料層應用程式精靈  
 **使用精靈註冊 DAC**  
  
1.  在 **[物件總管]** 中，展開含有要註冊為 DAC 的資料庫之執行個體的節點。  
  
2.  展開 **[資料庫]** 節點。  
  
3.  以滑鼠右鍵按一下要註冊的資料庫，然後指向 [工作]，再選取 [註冊為資料層應用程式…]  
  
4.  完成精靈對話方塊：  
  
    1.  [簡介頁面](#Introduction)  
  
    2.  [設定屬性頁面](#Set_properties)  
  
    3.  [驗證與摘要頁面](#Summary)  
  
    4.  [註冊 DAC 頁面](#Register)  
  
##  <a name="Introduction"></a> 簡介頁面  
 此頁面描述註冊資料層應用程式的步驟。  
  
 **不要再顯示此頁面。** - 按一下此核取方塊，之後就不會再顯示此頁面。  
  
 **下一步 >** - 繼續進行 [設定屬性] 頁面。  
  
 **取消** - 結束精靈，而不註冊 DAC。  
  
##  <a name="Set_properties"></a> 設定屬性頁面  
 使用此頁面來指定 DAC 層級屬性，例如應用程式名稱和版本。  
  
 **應用程式名稱** -指定用來識別 DAC 定義，欄位名稱的字串是已填入資料庫名稱。  
  
 **版本** - 可識別 DAC 版本的數值。 DAC 版本會用於 Visual Studio 中，以便識別開發人員正在處理的 DAC 版本。 在部署 DAC 時，版本會儲存在`msdb`資料庫和更新版本底下檢視**資料層應用程式**中的節點[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
 **描述** - 選擇性。 說明 DAC 用途的文字。 描述在部署 DAC 時，會儲存在`msdb`資料庫和更新版本底下檢視**資料層應用程式**中的節點[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。  
  
 **\< 先前**-會讓您回到**簡介**頁面。  
  
 **下一步 >** - 確認 DAC 可以從資料庫的物件建立而來，並在 [驗證與摘要] 頁面中顯示結果。  
  
 **取消** - 結束精靈，而不註冊 DAC。  
  
##  <a name="Summary"></a> 驗證與摘要頁面  
 使用此頁面來檢閱註冊 DAC 時，精靈將會採取的動作。 當精靈驗證可以從資料庫中的物件建立 DAC 時，此頁面會在三種狀態之間轉換。  
  
### <a name="retrieving-objects"></a>擷取物件  
 **擷取資料庫與伺服器物件。** - 當精靈從資料庫及 Database Engine 執行個體擷取所有必要的物件時，將會顯示進度列。  
  
 **\< 先前**-會讓您回到**器集合工具內容**頁面，以變更您的項目。  
  
 **下一步 >** - 註冊 DAC，並在 [註冊 DAC] 頁面中顯示結果。  
  
 **取消** - 結束精靈，而不註冊 DAC。  
  
### <a name="validating-objects"></a>驗證物件  
 **正在檢查**  *SchemaName* **＞。** *ObjectName* **＞。** - 當精靈驗證擷取之物件的相依性，並驗證這些對於 DAC 都是有效的物件時，將會顯示進度列。 *SchemaName ***.*** ObjectName* 識別目前正在驗證哪一個物件。  
  
 **\< 先前**-會讓您回到**器集合工具內容**頁面，以變更您的項目。  
  
 **下一步 >** - 註冊 DAC，並在 [註冊 DAC] 頁面中顯示結果。  
  
 **取消** - 結束精靈，而不註冊 DAC。  
  
### <a name="summary"></a>總結  
 **下列設定將用來註冊 DAC。** - 顯示將包含在 DAC 中的屬性和物件的報表。  
  
 **儲存報表** - 選取此按鈕可以將驗證報告複本儲存到 HTML 檔案。 預設資料夾為 Windows 帳戶之 [文件] 資料夾中的 **SQL Server Management Studio\DAC Packages** 資料夾。  
  
 **\< 先前**-會讓您回到**器集合工具內容**頁面，以變更您的項目。  
  
 **下一步 >** - 註冊 DAC，並在 [註冊 DAC] 頁面中顯示結果。  
  
 **取消** - 結束精靈，而不註冊 DAC。  
  
##  <a name="Register"></a> 註冊 DAC 頁面  
 此頁面會報告註冊作業成功或失敗。  
  
 **註冊 DAC** - 報告為了註冊 DAC 所採取的每個動作成功或失敗。 檢閱資訊以判斷每個動作成功或失敗。 發生錯誤的所有動作在 **[結果]** 資料行中都會有一個連結。 選取連結來檢視該動作的錯誤報告。  
  
 **儲存報表** - 選取此按鈕可以將註冊報告儲存到 HTML 檔案。 此檔案會報告每個動作的狀態，包括所有動作所產生的所有錯誤。 預設資料夾為 Windows 帳戶之 [文件] 資料夾中的 **SQL Server Management Studio\DAC Packages** 資料夾。 檔案名稱格式為 \<DACPackageName>_RegisterDACReport_yyyymmdd.html，其中 \<*DACPackageName*> 是要部署之套件的名稱、*yyyy* = 目前的年份、*mm* = 目前的月份，而 *dd* = 目前的日期。  
  
 **完成** - 結束精靈。  
  
##  <a name="RegisterDACPowerShell"></a> 使用 PowerShell 註冊 DAC  
 **若要在 PowerShell 指令碼中使用 Register() 方法，將資料庫註冊為 DAC**  
  
1.  建立 SMO Server 物件，並將它設定為包含要註冊為 DAC 之資料庫的執行個體。  
  
2.  加入可指定資料庫名稱的變數。  
  
3.  指定 DAC 的中繼資料，例如 DAC 名稱、版本及描述。  
  
4.  使用上述指定的資訊執行 Register 方法。  
  
### <a name="example-powershell"></a>範例 (PowerShell)  
 下列範例會將名稱為 MyDB 的資料庫註冊為 DAC。  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Specify the database to register as a DAC.  
$dbname = "MyDB"  
  
## Specify the DAC metadata.  
$applicationname = "MyApplication"  
$version = "1.0.0.0"  
$description = "This DAC defines the database used by my application."  
  
## Register the DAC.  
$registerunit = New-Object Microsoft.SqlServer.Management.Dac.DacExtractionUnit($srv, $dbname, $applicationname, $version)  
$registerunit.Description = $description  
$registerunit.Register()  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料層應用程式](data-tier-applications.md)  
  
  
