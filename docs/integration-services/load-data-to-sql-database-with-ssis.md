---
title: 使用 SQL Server Integration Services (SSIS) 將資料載入 SQL Server 或 Azure SQL Database | Microsoft Docs
description: 示範如何建立 SQL Server Integration Services (SSIS) 套件，將來自各種資料來源的資料移至 SQL Server 或 Azure SQL Database。
documentationcenter: NA
ms.prod: sql
ms.prod_service: integration-services
ms.suite: sql
ms.technology: integration-services
ms.devlang: NA
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.custom: loading
ms.date: 08/20/2018
ms.author: douglasl
author: douglaslMS
manager: craigg-msft
ms.openlocfilehash: ab5ce3238285cbe687b2608edb5236d460baa197
ms.sourcegitcommit: 9cd01df88a8ceff9f514c112342950e03892b12c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2018
ms.locfileid: "40405798"
---
# <a name="load-data-into-sql-server-or-azure-sql-database-with-sql-server-integration-services-ssis"></a>使用 SQL Server Integration Services (SSIS) 將資料載入 SQL Server 或 Azure SQL Database

建立 SQL Server Integration Services (SSIS) 套件，將資料載入 SQL Server 或 [Azure SQL Database](/azure/sql-database/)。 您也可以選擇在資料通過 SSIS 資料流程時，對它們進行架構重組、轉換及清理。

本文示範如何執行下列作業：

* 在 Visual Studio 中建立新的 Integration Services 專案。
* 設計可將資料從來源載入至目的地的 SSIS 套件。
* 執行 SSIS 套件以載入資料。


## <a name="basic-concepts"></a>基本概念

套件是 SSIS 中的基本工作單位。 相關聯的套件會在專案中組成群組。 您會在 Visual Studio 中使用 SQL Server Data Tools 來建立專案和設計套件。 設計程序是視覺化的程序，您可以從工具箱將元件拖放到設計介面，將它們連接，並設定其屬性。 當您完成您的套件之後，除能加以執行，也可選擇是否要將其部署到 SQL Server 或 SQL Database，以達到全面性管理、監視及安全性的目的。

SSIS 的詳細簡介超出本文範圍。 如需詳細資訊，請參閱下列文章：

- [SQL Server Integration Services](sql-server-integration-services.md)

- [如何建立 ETL 套件](ssis-how-to-create-an-etl-package.md)

## <a name="about-the-solution"></a>關於解決方法

此解決方法採用一般套件，會使用內含來源與目的地的資料流程工作。 此方法支援許多種資料來源，包括 SQL Server 與 Azure SQL Database。

本教學課程使用 SQL Server 作為資料來源。 SQL Server 會在內部部署或 Azure 虛擬機器上執行。

若要連線到 SQL Server 與 SQL Database，可以使用 ADO.NET 連線管理員加上來源與目的地，或使用 OLE DB 連線管理員加上來源與目的地。 本教學課程採用 ADO.NET，因為它的設定選項最少。 OLE DB 會提供比 ADO.NET 稍微更好的效能。

捷徑是使用 [SQL Server 匯入和匯出精靈] 來建立基本套件。 然後，儲存套件，並在 Visual Studio 或 SSDT 中開啟以進行檢視和自訂。 如需詳細資訊，請參閱[使用 SQL Server 匯入和匯出精靈匯入和匯出資料](import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)。

## <a name="prerequisites"></a>Prerequisites
若要逐步執行本教學課程，您需要下列項目：

1. **SQL Server Integration Services (SSIS)**。 SSIS 是 SQL Server 的元件，並且需要 SQL Server 的授權版本或是開發人員或評估版本。 若要取得 SQL Server 的評估版本，請參閱[評估 SQL Server](https://www.microsoft.com/evalcenter/evaluate-sql-server-2017-rtm)。
2. **Visual Studio** (選擇性)。 若要取得免費的 Visual Studio Community Edition，請參閱 [Visual Studio Community][Visual Studio Community]。 如果您不想要安裝 Visual Studio，您可以只安裝 SQL Server Data Tools (SSDT)。 SSDT 會安裝具有有限功能的 Visual Studio 版本。
3. **適用於 Visual Studio 的 SQL Server Data Tools (SSDT)**。 若要取得適用於 Visual Studio 的 SQL Server Data Tools，請參閱[下載 SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)]。
4. 本教學課程會連線到 SQL Server 或 SQL Database 執行個體，並將資料載入其中。 您必須具有連線、建立資料表以及對下列其中一項載入資料的權限：
   - **Azure SQL Database 資料庫**。 如需詳細資訊，請參閱 [Azure SQL Database](/azure/sql-database/)。  
      中的多個
   - **SQL Server 執行個體**。 SQL Server 會在內部部署或 Azure 虛擬機器上執行。 若要下載免費評估或開發人員版本的 SQL Server，請參閱 [SQL Server 下載](https://www.microsoft.com/sql-server/sql-server-downloads)。

5. **範例資料**。 本教學課程使用儲存在 SQL Server 的 AdventureWorks 範例資料庫內的範例資料，作為來源資料。 若要取得 AdventureWorks 範例資料庫，請參閱 [AdventureWorks 範例資料庫][AdventureWorks 2014 Sample Databases]。
6. 如果您將資料載入至 SQL Database，則為**防火牆規則**。 您必須先在 SQL Database 上，為您本機電腦的 IP 位址建立防火牆規則，然後才能將資料上傳到 SQL Database。

## <a name="create-a-new-integration-services-project"></a>建立新的 Integration Services 專案
1. 啟動 Visual Studio。
2. 在 [檔案] 功能表上，選取 [新增 | 專案]。
3. 瀏覽至 [已安裝 | 範本 | 商業智慧 | Integration Services] 專案類型。
4. 選取 [Integration Services 專案]。 為 [名稱] 和 [位置] 提供值，然後選取 [確定]。

Visual Studio 會開啟並建立新的 Integration Services (SSIS) 專案。 然後，Visual Studio 會為專案中新的單一 SSIS 套件 (Package.dtsx) 開啟設計工具。 您會看到下列畫面區域：

* 左側是 SSIS 元件的 [工具箱]。
* 中間是有許多索引標籤的設計介面。 一般來說，您至少會使用 [控制流程] 和 [資料流程] 索引標籤。
* 右側是 [方案總管] 和 [屬性] 窗格。
  
    ![][01]

## <a name="create-the-basic-data-flow"></a>建立基本資料流程
1. 將 [資料流程工作] 從 [工具箱] 拖曳至設計介面的中央 (在 [控制流程] 索引標籤上)。
   
    ![][02]
2. 按兩下 [資料流程工作] 以切換到 [資料流程] 索引標籤。
3. 從 [工具箱] 的 [其他來源] 清單中，將 [ADO.NET 來源] 拖曳至設計介面。 保持選取來源配接器，在 [屬性] 窗格中將其名稱變更為 **SQL Server 來源**。
4. 從 [工具箱] 的 [其他目的地] 清單中，將 [ADO.NET 目的地] 拖曳至設計介面的 [ADO.NET 來源] 底下。 選取目的地配接器，然後在 [屬性] 窗格中將其名稱變更為 [SQL 目的地]。
   
    ![][09]

## <a name="configure-the-source-adapter"></a>設定來源配接器
1. 按兩下來源配接器以開啟 [ADO.NET 來源編輯器]。
   
    ![][03]
2. 在 [ADO.NET 來源編輯器] 的 [連線管理員] 索引標籤上，按一下 [ADO.NET 連線管理員] 清單旁的 [新增] 按鈕，以開啟 [設定 ADO.NET 連線管理員] 對話方塊，然後針對本教學課程載入資料的來源 SQL Server 資料庫建立連線設定。
   
    ![][04]
3. 在 [設定 ADO.NET 連線管理員] 對話方塊中，按一下 [新增] 按鈕以開啟 [連線管理員] 對話方塊並建立新的資料連線。
   
    ![][05]
4. 在 [連線管理員] 對話方塊中，執行下列事項。
   
   1. 針對 [提供者]，選取 [SqlClient 資料提供者]。
   2. 針對 [伺服器名稱]，輸入 SQL Server 名稱。
   3. 在 [登入伺服器] 區段中，選取或輸入驗證資訊。
   4. 在 [連線到資料庫] 區段中，選取 [AdventureWorks 範例資料庫]。
   5. 按一下 **[測試連接]**。
      
       ![][06]
   6. 在報告連線測試結果的對話方塊中，按一下 [確定] 以返回 [連線管理員] 對話方塊。
   7. 在 [連線管理員] 對話方塊中，按一下 [確定] 以返回 [設定 ADO.NET 連線管理員] 對話方塊。
5. 在 [設定 ADO.NET 連線管理員] 對話方塊中，按一下 [確定] 以返回 [ADO.NET 來源編輯器]。
6. 在 [ADO.NET 來源編輯器] 的 [資料表或檢視的名稱] 清單中，選取 [Sales.SalesOrderDetail] 資料表。
   
    ![][07]
7. 按一下 [預覽] 以在 [預覽查詢結果] 對話方塊中查看來源資料表中的前 200 個資料列資料。
   
    ![][08]
8. 在 [預覽查詢結果] 對話方塊中，按一下 [關閉] 以返回 [ADO.NET 來源編輯器]。
9. 在 [ADO.NET 來源編輯器] 中，按一下 [確定] 以完成設定資料來源。

## <a name="connect-the-source-adapter-to-the-destination-adapter"></a>將來源配接器連線到目的地配接器
1. 在設計介面上選取來源配接器。
2. 選取從來源配接器延伸的藍色箭頭，並將它拖曳到目的地編輯器，直到它貼齊固定。
   
    ![][10]
   
    在一般的 SSIS 套件中，您可以在來源和目的地之間使用 SSIS 工具箱中的數個其他元件，以在資料通過 SSIS 資料流程時進行架構重組、轉換和清理。 為了盡可能使此範例簡單，我們會將來源直接連線到目的地。

## <a name="configure-the-destination-adapter"></a>設定目的地配接器
1. 按兩下目的地配接器以開啟 [ADO.NET 目的地編輯器]。
   
    ![][11]
2. 在 [ADO.NET 目的地編輯器] 的 [連線管理員] 索引標籤上，按一下 [連線管理員] 清單旁的 [新增] 按鈕，以開啟 [設定 ADO.NET 連線管理員] 對話方塊，然後針對本教學課程載入資料的目的地資料庫建立連線設定。
3. 在 [設定 ADO.NET 連線管理員] 對話方塊中，按一下 [新增] 按鈕以開啟 [連線管理員] 對話方塊並建立新的資料連線。
4. 在 [連線管理員] 對話方塊中，執行下列事項。
   1. 針對 [提供者]，選取 [SqlClient 資料提供者]。
   2. 針對 [伺服器名稱]，輸入 SQL Server 或 SQL Database 伺服器的名稱。
   3. 在 [登入伺服器] 區段中，選取 [使用 SQL Server 驗證] 並輸入驗證資訊。
   4. 在 [連線至資料庫] 區段中，選取現有資料庫。
    A. 按一下 **[測試連接]**。
    B. 在報告連線測試結果的對話方塊中，按一下 [確定] 以返回 [連線管理員] 對話方塊。
    c. 在 [連線管理員] 對話方塊中，按一下 [確定] 以返回 [設定 ADO.NET 連線管理員] 對話方塊。
5. 在 [設定 ADO.NET 連線管理員] 對話方塊中，按一下 [確定] 以返回 [ADO.NET 目的地編輯器]。
6. 在 [ADO.NET 目的地編輯器] 中，按一下 [使用資料表或檢視] 清單旁的 [新增] 以開啟 [建立資料表] 對話方塊，並使用與來源資料表相符的資料行清單建立新的目的地資料表。
   
    ![][12a]
7. 在 [建立資料表] 對話方塊中，執行下列事項。
   
   1. 將目的地資料表的名稱變更為 **SalesOrderDetail**。
      
       ![][12b]

   2. 按一下 [確定] 以建立資料表，並返回 [ADO.NET 目的地編輯器]。
8. 在 [ADO.NET 目的地編輯器] 中，選取 [對應] 索引標籤以查看來源中的資料行如何對應至目的地中的資料行。
   
    ![][13]
9. 按一下 [確定]，以完成目的地設定。

## <a name="run-the-package-to-load-the-data"></a>執行套件以載入資料
按一下工具列上的 [啟動] 按鈕，或選取 [偵錯] 功能表上的其中一個 [執行] 選項來執行套件。

以下段落描述使用本文所述的第二個選項 (也就是包含來源和目的地的資料流程) 建立套件時所看到的情況。

當套件開始執行時，您會看到黃色旋轉的轉輪表示活動，以及目前為止所處理的資料列數目。

![][14]

當套件完成執行時，您會看到綠色核取記號表示已成功，以及從來源載入至目的地的資料列總數。

![][15]

恭喜！ 您已成功使用 SQL Server Integration Services，將資料載入 SQL Server 或 Azure SQL Database。

## <a name="next-steps"></a>後續步驟

- 了解如何直接在設計環境中針對您的套件進行偵錯及疑難排解。 從這裡開始：[套件開發的疑難排解工具][Troubleshooting Tools for Package Development]。

- 了解如何將您的 SSIS 專案和套件部署到 Integration Services 伺服器或另一個儲存位置。 從這裡開始：[部署專案和套件][Deployment of Projects and Packages]。

<!-- Image references -->
[01]:  ./media/load-data-to-sql-database-with-ssis/ssis-designer-01.png
[02]:  ./media/load-data-to-sql-database-with-ssis/ssis-data-flow-task-02.png
[03]:  ./media/load-data-to-sql-database-with-ssis/ado-net-source-03.png
[04]:  ./media/load-data-to-sql-database-with-ssis/ado-net-connection-manager-04.png
[05]:  ./media/load-data-to-sql-database-with-ssis/ado-net-connection-05.png
[06]:  ./media/load-data-to-sql-database-with-ssis/test-connection-06.png
[07]:  ./media/load-data-to-sql-database-with-ssis/ado-net-source-07.png
[08]:  ./media/load-data-to-sql-database-with-ssis/preview-data-08.png
[09]:  ./media/load-data-to-sql-database-with-ssis/source-destination-09.png
[10]:  ./media/load-data-to-sql-database-with-ssis/connect-source-destination-10.png
[11]:  ./media/load-data-to-sql-database-with-ssis/ado-net-destination-11.png
[12a]: ./media/load-data-to-sql-database-with-ssis/destination-query-before-12a.png
[12b]: ./media/load-data-to-sql-database-with-ssis/destination-query-after-12b.png
[13]:  ./media/load-data-to-sql-database-with-ssis/column-mapping-13.png
[14]:  ./media/load-data-to-sql-database-with-ssis/package-running-14.png
[15]:  ./media/load-data-to-sql-database-with-ssis/package-success-15.png

<!-- Article references -->

<!-- MSDN references -->
[Download SQL Server Data Tools (SSDT)]: ../ssdt/download-sql-server-data-tools-ssdt.md
[Data Flow]: ./data-flow/data-flow.md
[Troubleshooting Tools for Package Development]: ./troubleshooting/troubleshooting-tools-for-package-development.md
[Deployment of Projects and Packages]: ./packages/deploy-integration-services-ssis-projects-and-packages.md

<!--Other Web references-->
[Microsoft SQL Server 2017 Integration Services Feature Pack for Azure]: https://www.microsoft.com/download/details.aspx?id=54798
[SQL Server Evaluations]: https://www.microsoft.com/evalcenter/evaluate-sql-server-2017
[Visual Studio Community]: https://www.visualstudio.com/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Sample Databases]: https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks
