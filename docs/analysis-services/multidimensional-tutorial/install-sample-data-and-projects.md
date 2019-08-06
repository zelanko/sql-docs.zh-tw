---
title: 安裝 Analysis Services 範例資料和專案 |Microsoft Docs
ms.date: 05/06/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2c89ee3edf9338c4f74b0738d930ee74dbec7244
ms.sourcegitcommit: bcc3b2c7474297aba17b7a63b17c103febdd0af9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/05/2019
ms.locfileid: "68794986"
---
# <a name="install-sample-data-and-multidimensional-projects"></a>安裝範例資料和多維度專案 
[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

請使用本文中提供的指示與連結, 安裝 Analysis Services 教學課程中所使用的資料和專案檔案。 
  
## <a name="step-1-install-prerequisites"></a>步驟 1：安裝必要條件 
本教學課程中的課程假設您已安裝下列軟體。 您可以在單一電腦上安裝所有功能。 若要安裝這些功能，請執行 SQL Server 安裝程式，並從 [特徵選取] 頁面中選取這些功能。  
  
-   SQL Server Database Engine  
  
-   SQL Server Analysis Services  (SSAS) 
  
    Analysis Services 僅適用于下列版本:評估、企業、商業智慧、標準。 Azure Analysis Services 中不支援多維度模型。
  
    根據預設, Analysis Services 2016 和更新版本會安裝為表格式實例, 您可以在安裝精靈的 [伺服器設定] 頁面中選擇 [多維度伺服器模式] 來覆寫。
  
## <a name="step-2-download-and-install-developer-and-management-tools"></a>步驟 2：下載並安裝開發人員和管理工具
Visual Studio 的 SQL Server Data Tools (SSDT) 會與其他 SQL Server 功能分開下載並安裝。 用來建立 BI 模型和報表的設計工具和專案範本會包含在 SSDT for Visual Studio 2015 中, 或作為 Visual Studio 2017 的[Nuget 套件](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)。  
  
[下載 SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=827542)。   

SQL Server Management Studio (SSMS) 會與其他 SQL Server 功能分開下載並安裝。  

[下載 SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md)  

或者，當您進行教學課程時，考慮安裝 Excel 來瀏覽多維度資料。 安裝 Excel 時會啟用 [在 Excel 中進行分析] 功能，此功能會使用 [樞紐分析表] 欄位清單啟動 Excel，而這份清單會連接至您要建立的 Cube。 建議使用 Excel 瀏覽資料，因為您可以快速建立一個可讓您與資料互動的樞紐分析報表。  
  
或者，您可以使用內建到 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 的內建 MDX 查詢設計工具來瀏覽資料。 查詢設計工具會傳回相同的資料，但以一般資料列集呈現的資料除外。  
  
## <a name="step-3-install-databases"></a>步驟 3：安裝資料庫  
Analysis Services 多維度模型使用您從關聯式資料庫管理系統匯入的交易資料。 基於本教學課程的目的, 您會使用下列關係資料庫做為您的資料來源。  
  
-   **AdventureWorksDW2012 或更新版本**-這是在資料庫引擎實例上執行的關聯式資料倉儲。 它會提供您在整個教學課程中建立及部署之 Analysis Services 資料庫和專案所使用的原始資料。 本教學課程假設您使用的是 AdventureWorksDW2012, 但較新的版本可正常執行。
  
    您可以使用此範例資料庫[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]搭配和更新版本。 一般來說, 您應該使用符合資料庫引擎版本的範例資料庫版本。
  
若要安裝資料庫, 請執行下列動作:  
  
1.  從 GitHub 下載[AdventureWorksDW](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)資料庫備份。  
  
2.  將備份檔案複製到本機 SQL Server 資料庫引擎實例的資料目錄。
  
3.  啟動 SQL Server Management Studio，並連接到 Database Engine 執行個體。  
  
4.  還原資料庫。  
  
## <a name="step-4-grant-database-permissions"></a>步驟 4：授與資料庫許可權  
範例專案會使用指定匯入或處理資料所使用之安全性內容的資料來源模擬設定。 根據預設，模擬設定會指定 Analysis Services 服務帳戶來存取資料。 若要使用此預設設定, 您必須確定執行 Analysis Services 的服務帳戶擁有**AdventureWorksDW**資料庫的資料讀取器許可權。  
  
> [!NOTE]  
> 基於學習的目的，建議您使用預設服務帳戶模擬選項，並將資料讀取器權限授與 SQL Server 中的服務帳戶。 即使有其他可用的模擬選項，但並非所有選項都適用於處理作業。 具體而言，不支援使用目前使用者的認證進行處理的選項。  
  
1.  判斷服務帳戶。 您可以使用 SQL Server 組態管理員或 [服務] 主控台應用程式來檢視帳戶資訊。 如果您使用預設帳戶安裝 Analysis Services 做為預設執行個體，此服務就會當做 **NT Service\MSSQLServerOLAPService**執行。  
  
2.  在 Management Studio 中，連接到 Database Engine 執行個體。  
  
3.  展開 [安全性] 資料夾，以滑鼠右鍵按一下 [登入]，然後選取 [新增登入]。  
  
4.  在 [一般] 頁面的 [登入名稱] 中，輸入 **NT Service\MSSQLServerOLAPService** (或執行服務所使用的帳戶)。  
  
5.  按一下 [使用者對應]。  
  
6.  選取**AdventureWorksDW**資料庫旁邊的核取方塊。 角色成員資格應該會自動包含 **db_datareader** 和 **public**。 按一下 [確定]，接受預設值。  
  
## <a name="step-5-install-projects"></a>步驟 5：安裝專案  

教學課程包含範例專案，讓您可以對照完成的專案比較您的結果，或開始順序中比較後面的課程。  
  
1.  從 GitHub 上的 Analysis Services 範例的「艾德作品」頁面下載[adventure-works-multidimensional-tutorial-projects。](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks-analysis-services)  
  
    教學課程專案適用于[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]和更新版本。  
  
2.  將 .zip 檔案移至根磁碟機的正下方資料夾 (例如 C:\Tutorial)。 如果您嘗試將 [下載] 資料夾中的檔案解壓縮, 則此步驟會降低「路徑太長」錯誤。  
  
3.  解壓縮範例專案、以滑鼠右鍵按一下該檔案，然後選取 [全部解壓縮]。 解壓縮檔案之後, 您應該會有第1課、第2、3、5、6、7、8、9、10完成和第4課開始的資料夾。 
  
4.  移除這些檔案的唯讀權限。 以滑鼠右鍵按一下父資料夾, 選取 [**屬性**], 然後清除 [**唯讀**] 核取方塊。 按一下 [確定]。 將變更套用到此資料夾、子資料夾和檔案。  

5.  開啟與您所在課程對應的方案 (.sln) 檔案。 例如，在名為 "Lesson 1 Complete" 的資料夾中，您會開啟 Analysis Services Tutorial.sln 檔案。  
  
6.  部署解決方案, 以確認已正確設定資料庫許可權和伺服器位置資訊。  
  
    如果 Analysis Services 和 Database Engine 是當做預設執行個體 (MSSQLServer) 安裝，而且所有軟體都在相同的電腦上執行，則您可以按一下 [組建] 功能表上的 [部署方案]，以建立範例專案，並將其部署至本機 Analysis Services 執行個體。 在部署期間, 會從本機資料庫引擎實例上的**AdventureWorksDW**資料庫處理 (或匯入) 資料。 Analysis Services 實例上會建立新的 Analysis Services 資料庫, 其中包含從資料庫引擎中取出的資料。  
  
    如果出現錯誤，請檢閱先前有關設定資料庫權限的步驟。 另外，您可能也需要變更伺服器名稱。 預設伺服器名稱為 localhost。 如果您的伺服器是安裝在遠端電腦上，或是安裝成具名執行個體，則必須覆寫預設值，改為使用對您的安裝有效的伺服器名稱。 此外，如果伺服器位於遠端電腦上，您可能需要設定 Windows 防火牆，以允許存取伺服器。  
  
    用來連接 Database Engine 的伺服器名稱會指定在多維度方案的資料來源物件中 (Adventure Works 教學課程)，顯示在方案總管中。  
  
    用來連接 Analysis Services 的伺服器名稱會指定在專案 [屬性] 頁面的 [部署] 索引標籤中，也會出現在方案總管中。  
  
7.  在 SQL Server Management Studio 中，連接到 Analysis Services。 請確認名為 **Analysis Services 教學課程** 的資料庫正在伺服器上執行。  
  
## <a name="next-step"></a>下一步  
您現在可以使用此教學課程。 如需如何開始使用的詳細資訊，請參閱[多維度模型化 &#40;Adventure Works 教學課程&#41;](multidimensional-modeling-adventure-works-tutorial.md)。  
  
## <a name="see-also"></a>另請參閱  
[設定 Windows 防火牆以允許 Analysis Services 存取](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)  
[設定 Windows 防火牆以允許 SQL Server 存取](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)  
  
  
