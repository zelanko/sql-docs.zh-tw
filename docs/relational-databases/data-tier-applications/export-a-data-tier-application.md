---
description: 匯出資料層應用程式
title: 匯出資料層應用程式 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.exportdac.progress.f1
- sql13.swb.exportdac.summary.f1
- sql13.swb.exportdac.results.f1
- sql13.swb. exportdac.results.f1
- sql13.swb. exportdac.summary.f1
- sql13.swb. exportdac.settings.f1
- sql13.swb.exportdac.welcome.f1
- sql13.swb.exportdac.settings.f1
helpviewer_keywords:
- How to [DAC], export
- wizard [DAC], export
- export DAC
- data-tier application [SQL Server], export
ms.assetid: 61915bc5-0f5f-45ac-8cfe-3452bc185558
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2e4ad904176abdc4f714980cf1e242bd620632a6
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97440212"
---
# <a name="export-a-data-tier-application"></a>匯出資料層應用程式
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  匯出已部署的資料層應用程式 (DAC) 或資料庫，會建立匯出檔，而此檔案包含資料庫中物件的定義以及資料表中所含的所有資料。 接著，匯出檔可以匯入 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的另一個執行個體或 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]。 您可以合併匯出/匯入作業，以在執行個體之間移轉 DAC、建立封存或針對 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]中所部署的資料庫建立內部部署複本。  
  
## <a name="before-you-begin"></a>開始之前  
 匯出程序會使用兩個階段來建立 DAC 匯出檔。  
  
1.  匯出會在匯出檔 (BACPAC 檔案) 中建置 DAC 定義，其方式相當於 DAC 擷取在 DAC 套件檔案中建置 DAC 定義。 匯出的 DAC 定義包含目前資料庫中的所有物件。 如果匯出程序是針對原本從 DAC 部署的資料庫來執行，並已在部署之後直接變更資料庫，則匯出的定義會符合資料庫中所設定的物件，而非原始 DAC 中所定義的物件。  
  
2.  匯出會大量複製資料庫中所有資料表的資料，並將資料合併至匯出檔。  

 匯出程序會將 DAC 版本設定為 1.0.0.0，而將匯出檔中的 DAC 描述設定為空字串。 如果已從 DAC 部署資料庫，則匯出檔中的 DAC 定義會包含指定給原始 DAC 的名稱，否則，DAC 名稱會設定為資料庫名稱。  
  

###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> 限制事項  
 DAC 或資料庫只能從 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]或 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) 或更新版本的資料庫中匯出。  
  
 如果 DAC 或包含的使用者中不支援資料庫的物件，則無法匯出資料庫。 如需有關 DAC 中支援之物件類型的詳細資訊，請參閱＜ [DAC Support For SQL Server Objects and Versions](/previous-versions/sql/sql-server-2012/ee210549(v=sql.110))＞。  
  
###  <a name="permissions"></a><a name="Permissions"></a> 權限  
 您至少需具備 ALTER ANY LOGIN 和資料庫範圍 VIEW DEFINITION 權限，以及 **sys.sql_expression_dependencies** 的 SELECT 權限，才能匯出 DAC。 匯出 DAC 可以透過 securityadmin 固定伺服器角色的成員來完成，這個角色的成員也是匯出 DAC 之來源資料庫中 database_owner 固定資料庫角色的成員。 系統管理員固定伺服器角色的成員或內建 SQL Server 系統管理員帳戶 **sa** 也可以匯出 DAC。
 
在 Azure SQL Database 上，您需要 **針對每個資料庫** 授與所有資料表或特定資料表的 VIEW DEFINITION 與 SELECT 權限

  
##  <a name="using-the-export-data-tier-application-wizard"></a><a name="UsingDeployDACWizard"></a> 使用匯出資料層應用程式精靈  
 **若要使用精靈匯出 DAC**  
  
1.  連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體 (不論是內部部署或在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]中)。  
  
2.  在物件總管  中，展開您要匯出 DAC 的執行個體來源節點。  
  
3.  以滑鼠右鍵按一下資料庫名稱。  
  
4.  按一下 [工作]  ，然後選取 [匯出資料層應用程式...]   
  
5.  完成精靈對話方塊：  
  
    -   [簡介頁面](#Introduction)  
  
    -   [匯出設定頁面](#Export_settings)  
  
    -   [驗證頁面](#Validation)  
  
    -   [摘要頁面](#Summary)  
  
    -   [進度頁面](#Progress)  
  
    -   [結果頁面](#Results)  
  
##  <a name="introduction-page"></a><a name="Introduction"></a> 簡介頁面  
 此頁面描述匯出資料層應用程式精靈的步驟。  
  
 **選項**  
  
 **不要再顯示此頁面。** - 按一下此核取方塊，之後就不會再顯示 [簡介] 頁面。  
  
 **下一步** - 繼續進行 [Select DAC Package (選取 DAC 封裝)]  頁面。  
  
 **取消** - 取消作業並關閉精靈。  
  
##  <a name="export-settings-page"></a><a name="Export_settings"></a> 匯出設定頁面  
 請使用此頁面來指定要建立 BACPAC 檔案的位置。  
  
-   **儲存至本機磁碟** - 在本機電腦的目錄中建立 BACPAC 檔案。 按一下 [瀏覽...]  巡覽本機電腦，或在提供的空間中指定路徑。 路徑名稱必須包含檔案名稱和 .bacpac 副檔名。  
  
-   **儲存至 Azure** - 在 Azure 容器中建立 BACPAC 檔案。 您必須連線到 Azure 容器，才能驗證此選項。 請注意，此選項也會要求您指定暫存檔的本機目錄。 請注意，暫存檔將建立在指定的位置，而且作業完成之後，將保留在該位置。  
  
 若要指定要匯出的資料表子集，請使用 [進階]  選項。  
  
##  <a name="validation-page"></a><a name="Validation"></a> 驗證頁面  
 您可以使用 [驗證] 頁面來檢閱封鎖作業的任何問題。 若要繼續進行，請解決封鎖問題，然後按一下 **[重新執行驗證]** 確定驗證成功。  
  
 若要繼續進行，請按 **[下一步]** 。  
  
##  <a name="summary-page"></a><a name="Summary"></a> 摘要頁面  
 您可以使用此頁面來檢閱作業的指定來源和目標設定。 若要使用指定的設定來完成匯出作業，請按一下 [完成]  。 若要取消匯出作業並結束精靈，請按一下 [取消]  。  
  
##  <a name="progress-page"></a><a name="Progress"></a> 進度頁面  
 此頁面會顯示進度列，指出作業的狀態。 若要檢視詳細狀態，請按一下 **[檢視詳細資料]** 選項。  
  
##  <a name="results-page"></a><a name="Results"></a> 結果頁面  
 此頁面會報告匯出作業成功或失敗，並顯示每個動作的結果。 發生錯誤的所有動作在 **[結果]** 資料行中都會有一個連結。 按一下連結，即可檢視該動作的錯誤報告。  
  
 按一下 **[完成]** 關閉精靈。  
  
##  <a name="using-a-net-framework-application"></a><a name="NetApp"></a> 使用 .Net Framework 應用程式  
 **在 .Net Framework 應用程式中使用 Export() 方法，匯出 DAC。**  
  
 若要檢視程式碼範例，請下載 [Codeplex](https://go.microsoft.com/fwlink/?LinkId=219575)上的 DAC 範例應用程式。  
  
1.  建立 SMO Server 物件，並將它設定為包含要匯出之 DAC 的執行個體。  
  
2.  開啟 **ServerConnection** 物件，並連接到相同的執行個體。  
  
3.  使用 **Microsoft.SqlServer.Management.Dac.DacStore** 類型的 **Export** 方法，匯出 DAC。 指定要匯出之 DAC 的名稱，以及要放置匯出檔之資料夾的路徑。  
  
## <a name="see-also"></a>另請參閱  
 [資料層應用程式](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [從資料庫中擷取 DAC](../../relational-databases/data-tier-applications/extract-a-dac-from-a-database.md)  
  
