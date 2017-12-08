---
title: "安裝 Sample Data and Projects |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: fc475b25-cbb2-408a-901f-9299299538c5
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Active
ms.openlocfilehash: 0e675845383c3e54c8477a8e0866231ac302cd1f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="install-sample-data-and-projects"></a>安裝 Sample Data and Projects 
使用本主題中提供的指示與連結，安裝 Analysis Services 教學課程中所使用的所有資料和專案檔案。  
  
## <a name="step-1-install-sql-server-software"></a>步驟 1：安裝 SQL Server 軟體  
本教學課程中的課程假設您已安裝下列軟體。 下列所有軟體都是使用 SQL Server 安裝媒體進行安裝。 為簡化部署，您可以在一台電腦上安裝所有功能。 若要安裝這些功能，請執行 SQL Server 安裝程式，並從 [特徵選取] 頁面中選取這些功能。 如需詳細資訊，請參閱 [從安裝精靈安裝 SQL Server 2016 &#40;安裝程式&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)。  
  
-   Database Engine  
  
-   Analysis Services  
  
    Analysis Services 僅適用於下列版本：Evaluation、Enterprise、Business Intelligence、Standard。  
  
    請注意，SQL Server Express 版本不包含 Analysis Services。 如果您想要免費試用軟體，請[下載 Evaluation Edition](http://go.microsoft.com/fwlink/?LinkId=392824) 。  
  
    根據預設，Analysis Services 會安裝成多維度執行個體，您可以在 [安裝精靈] 的伺服器組態頁面中選擇 [表格式伺服器模式] 來覆寫。 如果您想要同時執行兩種伺服器模式，請在相同電腦上重新執行 SQL Server 安裝程式，以另一個模式來安裝第二個 Analysis Services 執行個體。  
  
-   Transact-SQL  
  
或者，當您進行教學課程時，考慮安裝 Excel 來瀏覽多維度資料。 安裝 Excel 時會啟用 [在 Excel 中進行分析] 功能，此功能會使用 [樞紐分析表] 欄位清單啟動 Excel，而這份清單會連接至您要建立的 Cube。 建議使用 Excel 瀏覽資料，因為您可以快速建立一個可讓您與資料互動的樞紐分析報表。  
  
或者，您可以使用內建到 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]的內建 MDX 查詢設計工具來瀏覽資料。 查詢設計工具會傳回相同的資料，但以一般資料列集呈現的資料除外。  
  
## <a name="step-2-download-sql-server-data-tools-for-visual-studio-2015"></a>步驟 2：下載適用於 Visual Studio 2015 的 SQL Server Data Tools  
在此版本中，SQL Server Data Tools 要與其他 SQL Server 功能分開下載及安裝。 您可以在網路上免費下載用來建立 BI 模型和報表的設計工具和專案範本。  
  
-   [下載 SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=827542)。 檔案會儲存至 Downloads 資料夾。 執行安裝程式來安裝該工具。  
  
    重新開機以完成安裝。  
  
## <a name="step-3-install-databases"></a>步驟 3：安裝資料庫  
Analysis Services 多維度模型使用您從關聯式資料庫管理系統匯入的交易資料。 基於這個教學課程的目的，您將使用下列關聯式資料庫做為您的資料來源。  
  
-   **AdventureWorksDW2012** – 這是在 Database Engine 執行個體上執行的關聯式資料倉儲。 它提供 Analysis Services 資料庫將使用的原始資料，以及您在整個教學課程中建立與部署的專案。  
  
    您可以將這個範例資料庫用於 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 和 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]。  
  
若要安裝此資料庫，請執行下列動作：  
  
1.  從 codeplex 的產品範例頁面下載 [AdventureWorkDW2012](http://go.microsoft.com/fwlink/p/?LinkID=221770) 資料庫。  
  
    此資料庫檔案名稱為 AdvntureWorksDW2012_Data.mdf。 此檔案應該在您電腦的 [下載] 資料夾中。  
  
2.  將 AdventureWorksDW2012_Data.mdf 檔案複製到本機 SQL Server Database Engine 執行個體的資料目錄中。 根據預設，它位於 C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data。  
  
3.  啟動 SQL Server Management Studio，並連接到 Database Engine 執行個體。  
  
4.  以滑鼠右鍵按一下 [資料庫]，然後按一下 [附加]。  
  
5.  按一下 **[加入]**。  
  
6.  選取 **AdventureWorksDW2012_Data.mdf** 資料庫檔案，然後按一下 [確定]。 如果未列出檔案，請檢查 C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Data 資料夾以確認該檔案位於該處。  
  
7.  在資料庫詳細資料中，移除記錄檔項目。 安裝程式會假設您有記錄檔，但是範例中並沒有記錄檔。 附加資料庫時，將自動建立新的記錄檔。 選取記錄檔，並按一下 [移除]，然後按一下 [確定]，即可只附加主要資料庫檔案。  
  
## <a name="step-4-grant-database-permissions"></a>步驟 4：授與資料庫權限  
範例專案會使用指定匯入或處理資料所使用之安全性內容的資料來源模擬設定。 根據預設，模擬設定會指定 Analysis Services 服務帳戶來存取資料。 若要使用此預設設定，您必須確認執行 Analysis Services 所使用的服務帳戶擁有 **AdventureWorksDW2012** 資料庫的資料讀取器權限。  
  
> [!NOTE]  
> 基於學習的目的，建議您使用預設服務帳戶模擬選項，並將資料讀取器權限授與 SQL Server 中的服務帳戶。 即使有其他可用的模擬選項，但並非所有選項都適用於處理作業。 具體而言，不支援使用目前使用者的認證進行處理的選項。  
  
1.  判斷服務帳戶。 您可以使用 SQL Server 組態管理員或 [服務] 主控台應用程式來檢視帳戶資訊。 如果您使用預設帳戶安裝 Analysis Services 做為預設執行個體，此服務就會當做 **NT Service\MSSQLServerOLAPService**執行。  
  
2.  在 Management Studio 中，連接到 Database Engine 執行個體。  
  
3.  展開 [安全性] 資料夾，以滑鼠右鍵按一下 [登入]，然後選取 [新增登入]。  
  
4.  在 [一般] 頁面的 [登入名稱] 中，輸入 **NT Service\MSSQLServerOLAPService** (或執行服務所使用的帳戶)。  
  
5.  按一下 [使用者對應]。  
  
6.  選取 **AdventureWorksDW2012** 資料庫旁邊的核取方塊。 角色成員資格應該會自動包含 **db_datareader** 和 **public**。 按一下 [確定]，接受預設值。  
  
## <a name="step-5-install-projects"></a>步驟 5：安裝專案  
教學課程包含範例專案，讓您可以對照完成的專案比較您的結果，或開始順序中比較後面的課程。  
  
第 4 課的專案檔案特別重要，因為它不僅為第 4 課而且還為所有後續課程提供了基礎。 與先前的專案檔案相較之下，教學課程中的步驟會導致完全相同的已完成專案檔案的副本，而第 4 課的範例專案包含新的模型資訊，您在第 1 課到第 3 課內建的模型中找不到該項資訊。 第 4 課會假設您要啟動下列下載中提供的範例專案檔案。  
  
1.  在 codeplex 的產品範例頁面上，下載 [Analysis Services 教學課程 SQL Server 2012](http://go.microsoft.com/fwlink/p/?LinkID=221866) 。  
  
    2012 教學課程對 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 版本有效。  
  
    “Analysis Services Tutorial SQL Server 2012.zip” 檔案將會儲存到您電腦的 Downloads 資料夾中。  
  
2.  將 .zip 檔案移至根磁碟機的正下方資料夾 (例如 C:\Tutorial)。 如果您嘗試解壓縮 [下載] 資料夾中的檔案，此步驟會防止「路徑太長」的錯誤。  
  
3.  解壓縮範例專案、以滑鼠右鍵按一下該檔案，然後選取 [全部解壓縮]。 解壓縮檔案之後，您應該已經在電腦上安裝下列專案：  
  
    -   第 1 課完成  
  
    -   第 2 課完成  
  
    -   第 3 課完成  
  
    -   第 4 課完成  
  
    -   第 4 課開始  
  
    -   第 5 課完成  
  
    -   第 6 課完成  
  
    -   第 7 課完成  
  
    -   第 8 課完成  
  
    -   第 9 課完成  
  
    -   第 10 課完成  
  
4.  移除這些檔案的唯讀權限。 以滑鼠右鍵按一下上層資料夾 "Analysis Services Tutorial SQL Server 2012"，選取 [屬性]，並清除 [唯讀] 的核取方塊。 按一下 **[確定]**。 將變更套用到此資料夾、子資料夾和檔案。  
  
5.  啟動 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]。  
  
6.  開啟對應至您要使用之課程的方案 (.sln) 檔案。 例如，在名為 "Lesson 1 Complete" 的資料夾中，您會開啟 Analysis Services Tutorial.sln 檔案。  
  
7.  部署方案以確認已正確設定資料庫權限和伺服器位置資訊。  
  
    如果 Analysis Services 和 Database Engine 是當做預設執行個體 (MSSQLServer) 安裝，而且所有軟體都在相同的電腦上執行，則您可以按一下 [組建] 功能表上的 [部署方案]，以建立範例專案，並將其部署至本機 Analysis Services 執行個體。 在部署期間，資料將會從本機 Database Engine 執行個體上的 **AdventureWorksDW2012** 資料庫處理 (或匯入)。 Analysis Services 執行個體上將會建立新的 Analysis Services 資料庫，其中包含從 Database Engine 擷取的資料。  
  
    如果出現錯誤，請檢閱先前有關設定資料庫權限的步驟。 另外，您可能也需要變更伺服器名稱。 預設伺服器名稱為 localhost。 如果您的伺服器是安裝在遠端電腦上，或是安裝成具名執行個體，則必須覆寫預設值，改為使用對您的安裝有效的伺服器名稱。 此外，如果伺服器位於遠端電腦上，您可能需要設定 Windows 防火牆，以允許存取伺服器。  
  
    用來連接 Database Engine 的伺服器名稱會指定在多維度方案的資料來源物件中 (Adventure Works 教學課程)，顯示在方案總管中。  
  
    用來連接 Analysis Services 的伺服器名稱會指定在專案 [屬性] 頁面的 [部署] 索引標籤中，也會出現在方案總管中。  
  
8.  在 SQL Server Management Studio 中，連接到 Analysis Services。 請確認名為 **Analysis Services 教學課程** 的資料庫正在伺服器上執行。  
  
## <a name="next-step"></a>下一個步驟  
您現在可以使用此教學課程。 如需如何開始使用的詳細資訊，請參閱[多維度模型化 &#40;Adventure Works 教學課程&#41;](../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)。  
  
## <a name="see-also"></a>請參閱＜  
[從安裝精靈安裝 SQL Server 2016 &#40;安裝程式&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)  
[設定 Windows 防火牆以允許 Analysis Services 存取](../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)  
[設定 Windows 防火牆以允許 SQL Server 存取](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)  
  
  
  
