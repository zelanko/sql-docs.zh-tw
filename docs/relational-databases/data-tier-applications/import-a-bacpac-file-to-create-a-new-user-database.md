---
description: 匯入 BACPAC 檔案以建立新的使用者資料庫
title: 匯入 BACPAC 檔案以建立新的使用者資料庫
ms.date: 06/03/2020
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb. importdac.results.f1
- sql13.swb.importdac.settings.f1
- sql13.swb.importdac.storagebrowser.f1
- sql13.swb.importdac.results.f1
- sql13.swb.importdac.progress.f1
- sql13.swb. importdac.summary.f1
- sql13.swb.importdac.summary.f1
- sql13.swb. importdac.progress.f1
- sql13.swb.importdac.welcome.f1
- sql13.swb. importdac.settings.f1
helpviewer_keywords:
- Data-tier application
- SQL Server DAC
- Migrate database
- DAC
ms.assetid: 736d8d9a-39f1-4bf8-b81f-2e56c134d12e
author: stevestein
ms.author: sstein
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ba8fee19e7b0530bc73157125a025d5a724cbc00
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97481439"
---
# <a name="import-a-bacpac-file-to-create-a-new-user-database"></a>匯入 BACPAC 檔案以建立新的使用者資料庫
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  匯入資料層應用程式 (DAC) 檔案 (.bacpac 檔案)，可在新的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體上，建立原始資料庫連同其資料的複本，或將該檔案匯入 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]。 匯出-匯入作業可以進行合併以在執行個體之間移轉 DAC 或資料庫，或建立邏輯備份 (例如建立 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 中所部署資料庫的內部部署複本)。  
  
## <a name="before-you-begin"></a>開始之前  
 匯入程序會使用兩個階段來建立新的 DAC。  
  
1.  匯入會使用儲存在匯出檔案中的 DAC 定義，建立新的 DAC 及相關聯的資料庫，其方式相當於 DAC 部署從 DAC 封裝檔案中的定義建立新的 DAC。  
  
2.  匯入會從匯出檔案大量複製資料。  

## <a name="sql-server-utility"></a>SQL Server 公用程式  
 如果您將 DAC 匯入至資料庫引擎執行個體，下次從執行個體將公用程式收集組傳送到公用程式控制點時，匯入的 DAC 就會合併至 SQL Server 公用程式。 然後 DAC 會出現在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] [公用程式總管]  的 [部署的資料層應用程式]  節點中，並在 [部署的資料層應用程式]  詳細資料頁面中報告。  
  
## <a name="database-options-and-settings"></a>資料庫選項和設定  
 根據預設，匯入期間建立的資料庫將會擁有 CREATE DATABASE 陳述式中的所有預設值，但是資料庫定序和相容性層級會設定為 DAC 匯出檔案中所定義的值。 DAC 匯出檔案使用原始資料庫中的值。  
  
 某些資料庫選項 (例如 TRUSTWORTHY、DB_CHAINING 和 HONOR_BROKER_PRIORITY) 無法在匯入過程中調整。 實體屬性 (如檔案群組數目或檔案數目和大小) 無法在匯入過程中更改。 匯入完成之後，您可以使用 ALTER DATABASE 陳述式、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 來調整資料庫。 如需詳細資訊，請參閱 [Databases](../../relational-databases/databases/databases.md)。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 DAC 可匯入至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]或執行 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Service Pack 4 (SP4) 或更新版本的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 執行個體。 如果您從更新版本匯出 DAC，則 DAC 可能會包含 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]不支援的物件。 您無法將這些 DAC 部署至 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]執行個體。  
  
## <a name="prerequisites"></a>必要條件  
 建議您不要匯入來源不明或來源不受信任的 DAC 匯出檔案。 這類檔案可能包含惡意程式碼，因此可能會執行非預期的 Transact-SQL 程式碼，或是修改結構描述而造成錯誤。 在您使用來源不明或來源不受信任的匯出檔案之前，請解除封裝 DAC 並檢查程式碼，例如預存程序和其他使用者定義的程式碼。 如需有關如何執行這些檢查的詳細資訊，請參閱＜ [Validate a DAC Package](validate-a-dac-package.md)＞。  
  
## <a name="security"></a>安全性  
 為了提高安全性，SQL Server 驗證登入會儲存在 DAC 匯出檔案中，而且沒有密碼。 當您匯入檔案之後，此登入會建立為停用的登入，而且會產生密碼。 若要啟用登入，請使用具有 ALTER ANY LOGIN 權限的登入進行登入，並使用 ALTER LOGIN 來啟用登入，然後指派可以傳達給使用者的新密碼。 Windows 驗證登入不需要這項處理，因為這類登入的密碼不是由 SQL Server 所管理。  
  
## <a name="permissions"></a>權限  
 只有 **系統管理員 (sysadmin)** 或 **serveradmin** 固定伺服器角色的成員，或是具有 **dbcreator** 固定伺服器角色且擁有 ALTER ANY LOGIN 權限的登入，才能匯入 DAC。 內建的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員帳戶 (名稱為 **sa** ) 也可以匯入 DAC。 將具有登入的 DAC 匯入至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] ，需要 loginmanager 或 serveradmin 角色的成員資格。 將不具有登入的 DAC 匯入至 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] ，需要 dbmanager 或 serveradmin 角色的成員資格。  
  
## <a name="using-the-import-data-tier-application-wizard"></a>使用匯入資料層應用程式精靈  
 **若要啟動此精靈，請使用下列步驟：**  
  
1.  連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體 (不論是內部部署或在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 中)。  
  
2.  在 **[物件總管]** 的 **[資料庫]** 上按一下滑鼠右鍵，然後選取 **[匯入資料層應用程式]** 功能表項目啟動精靈。  
  
3.  完成精靈對話方塊：  
  
    -   [簡介頁面](#Introduction)  
  
    -   [匯入設定頁面](#Import_settings)  
  
    -   [資料庫設定頁面](#Database_settings)  
  
    -   [摘要頁面](#Summary)  
  
    -   [進度頁面](#Progress)  
  
    -   [結果頁面](#Results)  
  
###  <a name="introduction-page"></a><a name="Introduction"></a> 簡介頁面  
 此頁面描述的是資料層應用程式匯入精靈的步驟。  
  
 **選項**  
  
-   **不要再顯示此頁面。** - 按一下此核取方塊，之後就不會再顯示 [簡介] 頁面。  
  
-   **下一步** - 繼續進行 [匯入設定] 頁面。  
  
-   **取消** - 取消作業並關閉精靈。  
  
###  <a name="import-settings-page"></a><a name="Import_settings"></a> 匯入設定頁面  
 您可以使用此頁面來指定要匯入之 .bacpac 檔案的位置。  
  
-   **從本機磁碟匯入** - 按一下 [瀏覽...] 巡覽本機電腦，或在提供的空間中指定路徑。 路徑名稱必須包含檔案名稱和 .bacpac 副檔名。  
  
-   **從 Azure 匯入** - 從 Microsoft Azure 容器匯入 BACPAC 檔案。 您必須連線到 Microsoft Azure 容器，才能驗證此選項。 請注意，[從 Azure 匯入] 選項也會要求您指定暫存檔案的本機目錄。 暫存檔將建立在指定的位置，而且作業完成之後，將保留在該位置。  
  
     瀏覽 Azure 時，您可以在單一帳戶中的容器之間切換。 您必須指定單一 .bacpac 檔案，才能繼續進行匯入作業。 您可以依照 [名稱]、[大小] 或 [修改日期] 排序資料行。  
  
     若要繼續進行，請指定要匯入的 .bacpac 檔案，然後按一下 **[開啟]**。  
  
###  <a name="database-settings-page"></a><a name="Database_settings"></a> 資料庫設定頁面  
 您可以使用此頁面指定要建立之資料庫的詳細資料。  
  
 **若為 SQL Server 的本機執行個體：**  
  
-   **新資料庫名稱** - 針對匯入的資料庫提供名稱。  
  
-   **資料檔案路徑** - 提供資料檔案的本機目錄。 按一下 [瀏覽...]  巡覽本機電腦，或在提供的空間中指定路徑。  
  
-   **記錄檔路徑** - 提供記錄檔的本機目錄。 按一下 [瀏覽...]  巡覽本機電腦，或在提供的空間中指定路徑。  
  
 若要繼續進行，請按 **[下一步]** 。  
  
 **針對 Azure SQL Database：**  
  
 - **[匯入 BACPAC 檔案以建立新的 Azure SQL Database](/azure/azure-sql/database/database-import)** 提供使用 Azure 入口網站、PowerShell、SSMS 或 SqlPackage 的逐步指示。  
 - 請參閱 **[SQL Database 選項和效能︰了解每個服務層的可用項目](/azure/azure-sql/database/purchasing-models)** ，以取得不同服務層的詳細外觀。  

### <a name="validation-page"></a>驗證頁面  
 您可以使用此頁面檢閱造成此作業無法執行的任何問題。 若要繼續進行，請解決封鎖問題，然後按一下 **[重新執行驗證]** 確定驗證成功。  
  
 若要繼續進行，請按 **[下一步]** 。  
  
###  <a name="summary-page"></a><a name="Summary"></a> 摘要頁面  
 您可以使用此頁面來檢閱作業的指定來源和目標設定。 若要使用指定的設定來完成匯入作業，請按一下 **[完成]**。 若要取消匯入作業並結束精靈，請按一下 **[取消]**。  
  
###  <a name="progress-page"></a><a name="Progress"></a> 進度頁面  
 此頁面會顯示進度列，指出作業的狀態。 若要檢視詳細狀態，請按一下 **[檢視詳細資料]** 選項。  
  
 若要繼續進行，請按 **[下一步]** 。  
  
###  <a name="results-page"></a><a name="Results"></a> 結果頁面  
 此頁面會報告匯入和建立資料庫作業成功或失敗，並顯示每個動作成功或失敗。 發生錯誤的所有動作在 **[結果]** 資料行中都會有一個連結。 按一下連結，即可檢視該動作的錯誤報告。  
  
 按一下 [關閉] 以關閉精靈。  
  
## <a name="see-also"></a>另請參閱  
[匯入 BACPAC 檔案以建立新的 Azure SQL 資料庫](/azure/azure-sql/database/database-import)  
 [資料層應用程式](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [匯出資料層應用程式](../../relational-databases/data-tier-applications/export-a-data-tier-application.md)  
  
