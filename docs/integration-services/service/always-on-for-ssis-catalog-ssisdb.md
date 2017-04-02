---
title: "Always On for SSIS Catalog (SSISDB) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.ssms.alwayson.f1"
ms.assetid: 7f089455-35ee-4c13-884e-9254b685d07d
caps.latest.revision: 17
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 16
---
# Always On for SSIS Catalog (SSISDB)
  AlwaysOn 可用性群組功能是提供資料庫鏡像之企業級替代方案的高可用性與災害復原解決方案。 可用性群組支援一組可一起容錯移轉之離散化使用者資料庫的容錯移轉環境，也就是所謂的可用性資料庫。 如需詳細資訊，請參閱 [AlwaysOn 可用性群組 (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx)。  
  
 為了提供 SSIS 目錄 (SSISDB) 及其內容 (專案、封裝、執行記錄等) 的高可用性，您可以將 SSISDB 資料庫 (就像任何其他使用者資料庫) 加入 AlwaysOn 可用性群組。 發生容錯移轉時，其中一個次要節點會自動變成新的主要節點。  
 
 > [!IMPORTANT]  在容錯移轉時，執行中的套件不會重新啟動或繼續。 
 
 **本主題內容：**  
  
1.  [必要條件](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#prereq)  
  
2.  [設定適用於 AlwaysOn 的 SSIS 支援](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Firsttime)  
  
3.  [在可用性群組中升級 SSISDB](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Upgrade)  
  
##  <a name="a-nameprereqa-prerequisites"></a><a name="prereq"></a> 必要條件  
 您必須執行下列必要條件步驟，才能針對 SSISDB 資料庫啟用 AlwaysOn 支援。  
  
1.  設定 Windows 容錯移轉叢集。 如需相關指示，請參閱 [安裝適用於 Windows Server 2012 的容錯移轉叢集功能和工具](http://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx) 部落格文章。 您應該在所有叢集節點上安裝此功能和工具。  
  
2.  在叢集的每個節點上，安裝含有 Integration Services (SSIS) 功能的 SQL Server 2016。  
  
3.  啟用每個 SQL Server 執行個體的 AlwaysOn 功能。 如需詳細資訊，請參閱 [啟用和停用 AlwaysOn 可用性群組 (SQL Server)](https://msdn.microsoft.com/library/ff878259.aspx) 。  
  
##  <a name="a-namefirsttimea-configure-ssis-support-for-always-on"></a><a name="Firsttime"></a> 設定適用於 AlwaysOn 的 SSIS 支援  
  
-   [步驟 1：建立 Integration Services 目錄](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Step1)  
  
-   [步驟 2：將 SSISDB 新增至 AlwaysOn 可用性群組](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Step2)  
  
-   [步驟 3：啟用適用於 AlwaysOn 的 SSIS 支援](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Step3)  
  
> [!IMPORTANT]  
>  -   您必須在可用性群組的 **主要節點** 上執行這些步驟。  
> -   當您將 SSISDB 加入 AlwaysOn 群組之後，必須啟用 **適用於 AlwaysOn 的 SSIS 支援** 。  
  
###  <a name="a-namestep1a-step-1-create-integration-services-catalog"></a><a name="Step1"></a> 步驟 1：建立 Integration Services 目錄  
  
1.  啟動 **SQL Server Management Studio** 並連接到您想要在叢集中設定為適用於 SSISDB 的 AlwaysOn 高可用性群組 **主要節點** 的 SQL Server 執行個體。  
  
2.  在物件總管中，展開伺服器節點，以滑鼠右鍵按一下 [Integration Services 目錄] 節點，然後按一下 [建立目錄]。  
  
3.  按一下 **[啟用 CLR 整合]**。 目錄便會使用 CLR 預存程序。  
  
4.  按一下 [在 SQL Server 啟動時允許自動執行 Integration Services 預存程序]  ，讓 [catalog.startup](https://msdn.microsoft.com/library/hh230984.aspx) 預存程序會在每次 SSIS 伺服器執行個體重新啟動時執行。 預存程序會執行 SSISDB 目錄之作業狀態的維護。 它會在 SSIS 伺服器執行個體效能降低時，修正任何正在執行之封裝的狀態。  
  
5.  輸入 **密碼**，然後按一下 [確定] 。 此密碼保護用來加密目錄資料的資料庫主要金鑰。 請將密碼儲存在安全位置。 建議您同時備份資料庫主要金鑰。 如需詳細資訊，請參閱 [備份資料庫主要金鑰](https://msdn.microsoft.com/library/aa337546.aspx)。  
  
###  <a name="a-namestep2a-step-2-add-ssisdb-to-an-always-on-availability-group"></a><a name="Step2"></a> 步驟 2：將 SSISDB 新增至 AlwaysOn 可用性群組  
 將 SSISDB 資料庫加入 AlwaysOn 可用性群組，幾乎等於是將任何其他使用者資料庫加入可用性群組。 請參閱 [使用可用性群組精靈](https://msdn.microsoft.com/library/hh403415.aspx)。  
  
 您需要提供您在 **新增可用性群組** 精靈的 [選取資料庫]  頁面中建立 SSIS 目錄時指定的密碼。  
  
 ![New Availability Group](../../integration-services/service/media/ssis-newavailabilitygroup.png "New Availability Group")  
  
###  <a name="a-namestep3a-step-3-enable-ssis-support-for-always-on"></a><a name="Step3"></a> 步驟 3：啟用適用於 AlwaysOn 的 SSIS 支援  
 建立 Integration Services 目錄之後，請以滑鼠右鍵按一下 [Integration Services 目錄] 節點，然後按一下 [啟用 AlwaysOn 支援...]。 您應該會看到下列 [啟用 AlwaysOn 支援] 對話方塊。 如果這個功能表項目已停用，請確認您已安裝的所有必要條件，然後按一下 [重新整理] 。  
  
 ![Enable Support for AlwaysOn](../../integration-services/service/media/ssis-enablesupportforalwayson.png "Enable Support for AlwaysOn")  
  
> [!WARNING]  
>  在您啟用適用於 AlwaysOn 的 SSIS 支援之前，不支援自動容錯移轉 SSISDB 資料庫。  
  
 來自 AlwayOn 可用性群組的新加入次要複本會顯示在資料表中。 按一下 **[連接]** 按鈕，然後輸入驗證認證以連接到複本。 使用者帳戶必須是每個複本上系統管理員群組的成員，才能啟用 SSIS AlwaysOn 支援。 當您成功連接到每個複本之後，按一下 [確定] 以啟用適用於 AlwaysOn 的 SSIS 支援。  
  
##  <a name="a-nameupgradea-upgrading-ssisdb-in-an-availability-group"></a><a name="Upgrade"></a> 在可用性群組中升級 SSISDB  
 如果您要從先前的版本升級 SQL Server，而且 SSISDB 在 AlwaysOn 可用性群組中，則您的升級可能會遭到「SSISDB 在 AlwaysOn 可用性群組中檢查」規則所封鎖。 因為升級是在單一使用者模式中執行，而可用性資料庫必須是多使用者資料庫，就會發生此封鎖。 因此，在升級或修補期間，所有的可用性資料庫 (包括 SSISDB) 都要離線，而且不會進行升級或修補。 若要讓升級繼續，您必須先從可用性群組移除 SSISDB，接著升級或修補每個節點，然後將 SSISDB 加回可用性群組。  
  
 如果您遭到「SSISDB 在 AlwaysOn 可用性群組中檢查」規則封鎖，就必須依照這些步驟來升級 SQL Server。  
  
1.  從可用性群組中移除 SSISDB 資料庫。 如需詳細資訊，請參閱[將次要資料庫從可用性群組移除 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-a-secondary-database-from-an-availability-group-sql-server.md) 和[將主要資料庫從可用性群組移除 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md)。  
  
2.  按一下升級精靈中的 [重新執行]。 「SSISDB 在 AlwaysOn 可用性群組中檢查」規則將會通過。  
  
3.  按 [下一步]  繼續升級。  
  
4.  當您已升級所有節點之後，請將 SSISDB 資料庫加回 AlwaysOn 可用性群組。 如需詳細資訊，請參閱[將資料庫加入至可用性群組 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/add-a-database-to-an-availability-group-sql-server.md)。  
  
 如果您在升級 SQL Server 時未遭到封鎖，且 SSISDB 在 AlwaysOn 可用性群組中，就必須在升級 SQL Server 資料庫引擎之後個別升級 SSISDB。 使用 SSIS 升級精靈來升級 SSISDB，如下列程序所述。  
  
1.  將 SSISDB 資料庫移出可用性群組，或者如果 SSISDB 是可用性群組中唯一的資料庫，請刪除可用性群組。 您必須在可用性群組的 **主要節點** 上啟動 **SQL Server Management Studio** ，來執行這項工作。  
  
2.  從所有 **複本節點**移除 SSISDB 資料庫。  
  
3.  在 **主要節點**上升級 SSISDB 資料庫。 在 SQL Server Management Studio 的物件總管中，展開 [Integration Services 目錄]、以滑鼠右鍵按一下 [SSISDB]，然後選取 [資料庫升級]。 遵循 **SSISDB 升級精靈** 中的指示來升級資料庫。 您必須在 **主要節點** 上本機啟動 **SSIDB 升級精靈**。  
  
4.  依照 [步驟 2：將 SSISDB 加入 AlwaysOn 可用性群組](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Step2) 的指示，將 SSISDB 加回可用性群組。  
  
5.  依照 [步驟 3：啟用適用於 AlwaysOn 的 SSIS 支援](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Step3)的指示。  
  
  