---
title: 安裝 Sample Data and Projects |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0ec266a98e3a27dd277ccd9f790ae73d1793ec38
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="install-sample-data-and-multidimensional-projects"></a>安裝範例資料和多維度專案 
[!INCLUDE[ssas-appliesto-sqlas-all](../includes/ssas-appliesto-sqlas-all.md)]

若要安裝 Analysis Services 教學課程中使用的資料和專案檔案使用的指示與本文章中提供的連結。 
  
## <a name="step-1-install-prerequisites"></a>步驟 1： 安裝必要條件 
本教學課程中的課程假設您已安裝下列軟體。 您可以在單一電腦上安裝的所有功能。 若要安裝這些功能，請執行 SQL Server 安裝程式，並從 [特徵選取] 頁面中選取這些功能。  
  
-   SQL Server Database Engine  
  
-   SQL Server Analysis Services (SSAS) 
  
    Analysis Services 僅適用於下列版本：Evaluation、Enterprise、Business Intelligence、Standard。 Azure Analysis Services 中不支援多維度模型。
  
    根據預設，Analysis Services 2016 和更新版本安裝為表格式執行個體，您可以選擇覆寫多維度伺服器模式中的伺服器安裝精靈的 [組態] 頁面。
  
## <a name="step-2-download-and-install-developer-and-management-tools"></a>步驟 2： 下載並安裝開發人員和管理工具
SQL Server Data Tools (SSDT) for Visual Studio 會下載並與其他 SQL Server 功能分開安裝。 設計工具和用來建立 BI 模型和報表的專案範本隨附的 SSDT for Visual Studio 2015 或[Nuget 封裝](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)for Visual Studio 2017。  
  
[下載 SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=827542)。   

SQL Server Management Studio (SSMS) 是下載及其他 SQL Server 功能分開安裝。  

[下載 SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)  

或者，當您進行教學課程時，考慮安裝 Excel 來瀏覽多維度資料。 安裝 Excel 時會啟用 [在 Excel 中進行分析] 功能，此功能會使用 [樞紐分析表] 欄位清單啟動 Excel，而這份清單會連接至您要建立的 Cube。 建議使用 Excel 瀏覽資料，因為您可以快速建立一個可讓您與資料互動的樞紐分析報表。  
  
或者，您可以使用內建到 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]的內建 MDX 查詢設計工具來瀏覽資料。 查詢設計工具會傳回相同的資料，但以一般資料列集呈現的資料除外。  
  
## <a name="step-3-install-databases"></a>步驟 3： 安裝資料庫  
Analysis Services 多維度模型使用您從關聯式資料庫管理系統匯入的交易資料。 基於本教學課程的目的，您可以使用下列關聯式資料庫做為資料來源。  
  
-   **AdventureWorksDW2012 或更新版本**– 這是 Database Engine 執行個體執行的關聯式資料倉儲。 它提供 Analysis Services 資料庫和專案的建置及部署整個教學課程所使用的原始資料。 本教學課程假設您使用的 AdventureWorksDW2012，不過，更新版本執行的工作。
  
    您可以使用這個範例資料庫用於[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]和更新版本。 在一般，您應該使用比對您的資料庫引擎版本範例資料庫版本。
  
若要安裝資料庫，執行下列作業：  
  
1.  下載[AdventureWorkDW](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)從 GitHub 的資料庫備份。  
  
2.  將備份檔案複製到本機 SQL Server Database Engine 執行個體的資料目錄。
  
3.  啟動 SQL Server Management Studio，並連接到 Database Engine 執行個體。  
  
4.  還原資料庫。  
  
## <a name="step-4-grant-database-permissions"></a>步驟 4： 授與資料庫權限  
範例專案會使用指定匯入或處理資料所使用之安全性內容的資料來源模擬設定。 根據預設，模擬設定會指定 Analysis Services 服務帳戶來存取資料。 若要使用此預設設定，您必須確定執行 Analysis Services 的服務帳戶具有資料讀取器權限**AdventureWorksDW**資料庫。  
  
> [!NOTE]  
> 基於學習的目的，建議您使用預設服務帳戶模擬選項，並將資料讀取器權限授與 SQL Server 中的服務帳戶。 即使有其他可用的模擬選項，但並非所有選項都適用於處理作業。 具體而言，不支援使用目前使用者的認證進行處理的選項。  
  
1.  判斷服務帳戶。 您可以使用 SQL Server 組態管理員或 [服務] 主控台應用程式來檢視帳戶資訊。 如果您使用預設帳戶安裝 Analysis Services 做為預設執行個體，此服務就會當做 **NT Service\MSSQLServerOLAPService**執行。  
  
2.  在 Management Studio 中，連接到 Database Engine 執行個體。  
  
3.  展開 [安全性] 資料夾，以滑鼠右鍵按一下 [登入]，然後選取 [新增登入]。  
  
4.  在 [一般] 頁面的 [登入名稱] 中，輸入 **NT Service\MSSQLServerOLAPService** (或執行服務所使用的帳戶)。  
  
5.  按一下 [使用者對應]。  
  
6.  選取此核取方塊旁的  **AdventureWorksDW**資料庫。 角色成員資格應該會自動包含 **db_datareader** 和 **public**。 按一下 [確定]，接受預設值。  
  
## <a name="step-5-install-projects"></a>步驟 5： 安裝專案  

教學課程包含範例專案，讓您可以對照完成的專案比較您的結果，或開始順序中比較後面的課程。  
  
1.  下載[adventure-works-多維度的教學課程-projects.zip](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks-analysis-services)從 Adventure Works 的 GitHub 上的 Analysis Services 範例頁面。  
  
    本教學課程專案的工作[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]和更新版本。  
  
2.  將 .zip 檔案移至根磁碟機的正下方資料夾 (例如 C:\Tutorial)。 如果您嘗試解壓縮 [下載] 資料夾中的檔案，此步驟會防止「路徑太長」的錯誤。  
  
3.  解壓縮範例專案、以滑鼠右鍵按一下該檔案，然後選取 [全部解壓縮]。 解壓縮檔案之後，您應該有資料夾課程 1、 2、 3、 5、 6、 7、 8、 9、 10 完成和 Lesson 4 Start。 
  
4.  移除這些檔案的唯讀權限。 以滑鼠右鍵按一下父資料夾中，選取**屬性**，清除核取方塊和**唯讀**。 按一下 **[確定]**。 將變更套用到此資料夾、子資料夾和檔案。  

5.  開啟對應於您是在本課程的方案 (.sln) 檔案。 例如，在名為 "Lesson 1 Complete" 的資料夾中，您會開啟 Analysis Services Tutorial.sln 檔案。  
  
6.  部署方案來驗證的資料庫權限和伺服器位置資訊都已正確設定。  
  
    如果 Analysis Services 和 Database Engine 是當做預設執行個體 (MSSQLServer) 安裝，而且所有軟體都在相同的電腦上執行，則您可以按一下 [組建] 功能表上的 [部署方案]，以建立範例專案，並將其部署至本機 Analysis Services 執行個體。 在部署期間，資料處理 （或匯入） 從**AdventureWorksDW**本機 Database Engine 執行個體上的資料庫。 包含從 Database Engine 擷取的資料的 Analysis Services 執行個體上建立新的 Analysis Services 資料庫。  
  
    如果出現錯誤，請檢閱先前有關設定資料庫權限的步驟。 另外，您可能也需要變更伺服器名稱。 預設伺服器名稱為 localhost。 如果您的伺服器是安裝在遠端電腦上，或是安裝成具名執行個體，則必須覆寫預設值，改為使用對您的安裝有效的伺服器名稱。 此外，如果伺服器位於遠端電腦上，您可能需要設定 Windows 防火牆，以允許存取伺服器。  
  
    用來連接 Database Engine 的伺服器名稱會指定在多維度方案的資料來源物件中 (Adventure Works 教學課程)，顯示在方案總管中。  
  
    用來連接 Analysis Services 的伺服器名稱會指定在專案 [屬性] 頁面的 [部署] 索引標籤中，也會出現在方案總管中。  
  
7.  在 SQL Server Management Studio 中，連接到 Analysis Services。 請確認名為 **Analysis Services 教學課程** 的資料庫正在伺服器上執行。  
  
## <a name="next-step"></a>下一步  
您現在可以使用此教學課程。 如需如何開始使用的詳細資訊，請參閱[多維度模型化 &#40;Adventure Works 教學課程&#41;](../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)。  
  
## <a name="see-also"></a>另請參閱  
[設定 Windows 防火牆以允許 Analysis Services 存取](../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)  
[設定 Windows 防火牆以允許 SQL Server 存取](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)  
  
  