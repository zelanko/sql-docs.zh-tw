---
title: 將資料從 SQL Server 載入 Azure SQL 資料倉儲 (SSIS) | Microsoft Docs
description: 示範如何建立 SQL Server Integration Services (SSIS) 套件，以將資料從各種資料來源移至 SQL 資料倉儲。
services: sql-data-warehouse
documentationcenter: NA
author: douglaslMS
manager: craigg-msft
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 04/04/2018
ms.author: douglasl
ms.openlocfilehash: 6be9111a29156c7bea74dc27bbb0ca5351259018
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="load-data-from-sql-server-to-azure-sql-data-warehouse-with-sql-server-integration-services-ssis"></a>使用 SQL Server Integration Services (SSIS) 將資料從 SQL Server 載入 Azure SQL 資料倉儲

建立 SQL Server Integration Services (SSIS) 套件，以將資料從 SQL Server 載入 [Azure SQL 資料倉儲](/azure/sql-data-warehouse/index.md)。 您也可以選擇在資料通過 SSIS 資料流程時，對它們進行架構重組、轉換及清理。

在本教學課程中，您將會：

* 在 Visual Studio 中建立新的 Integration Services 專案。
* 連線到資料來源，包括 SQL Server (作為來源) 以及 SQL 資料倉儲 (作為目的地)。
* 設計可將資料從來源載入至目的地的 SSIS 套件。
* 執行 SSIS 套件以載入資料。

本教學課程使用 SQL Server 作為資料來源。 SQL Server 可在內部部署或 Azure 虛擬機器中執行。

## <a name="basic-concepts"></a>基本概念
套件是 SSIS 中的工作單位。 相關聯的套件會在專案中組成群組。 您會在 Visual Studio 中使用 SQL Server Data Tools 來建立專案和設計套件。 設計程序是視覺化的程序，您可以從工具箱將元件拖放到設計介面，將它們連接，並設定其屬性。 在您完成套件之後，可以選擇將它部署到 SQL Server 以進行全方位的管理、監視和安全性。

## <a name="options-for-loading-data-with-ssis"></a>使用 SSIS 載入資料的選項
SQL Server Integration Services (SSIS) 是彈性的工具組，可提供各種不同選項以針對 SQL 資料倉儲進行連線和資料的載入。

1. 使用 ADO NET 目的地來連線到 SQL 資料倉儲。 本教學課程會使用 ADO NET 目的地，因為它具有最少的設定選項。
2. 使用 OLE DB 目的地來連線到 SQL 資料倉儲。 這個選項會提供比 ADO NET 目的地稍微更好的效能。
3. 使用 Azure Blob 上傳工作將資料暫存於 Azure Blob 儲存體。 然後使用 SSIS 執行 SQL 工作以啟動能將資料載入至 SQL 資料倉儲的 PolyBase 指令碼。 這個選項能提供此處所列三個選項當中最好的效能。 若要取得 Azure Blob 上傳工作，請下載[適用於 Azure 的 Microsoft SQL Server 2016 Integration Services 功能套件][Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]。 若要深入了解 PolyBase，請參閱 [PolyBase 指南][PolyBase Guide]。

## <a name="before-you-start"></a>開始之前
若要逐步執行本教學課程，您需要：

1. **SQL Server Integration Services (SSIS)**。 SSIS 是 SQL Server 的元件，並且需要評估版本或授權版本的 SQL Server。 若要取得 SQL Server 2016 Preview 的評估版本，請參閱 [SQL Server 評估版][SQL Server Evaluations]。
2. **Visual Studio**。 若要取得免費的 Visual Studio Community Edition，請參閱 [Visual Studio Community][Visual Studio Community]。
3. **適用於 Visual Studio 的 SQL Server Data Tools (SSDT)**。 若要取得適用於 Visual Studio 的 SQL Server Data Tools，請參閱[下載 SQL Server Data Tools (SSDT)][Download SQL Server Data Tools (SSDT)]。
4. **範例資料**。 本教學課程使用儲存在 SQL Server 中 AdventureWorks 範例資料庫內的範例資料，作為要載入 SQL 資料倉儲的來源資料。 若要取得 AdventureWorks 範例資料庫，請參閱 [AdventureWorks 2014 範例資料庫][AdventureWorks 2014 Sample Databases]。
5. **SQL 資料倉儲資料庫和權限**。 本教學課程會連線到 SQL 資料倉儲執行個體，並將資料載入至其中。 您必須有建立資料表和載入資料的權限。
6. **防火牆規則**。 您必須使用本機電腦的 IP 位址針對 SQL 資料倉儲建立防火牆規則，然後才能將資料上傳到 SQL 資料倉儲。

## <a name="step-1-create-a-new-integration-services-project"></a>步驟 1：建立新的 Integration Services 專案
1. 啟動 Visual Studio。
2. 在 [檔案] 功能表上，選取 [新增 | 專案]。
3. 瀏覽至 [已安裝 | 範本 | 商業智慧 | Integration Services] 專案類型。
4. 選取 [Integration Services 專案]。 為 [名稱] 和 [位置] 提供值，然後選取 [確定]。

Visual Studio 會開啟並建立新的 Integration Services (SSIS) 專案。 然後，Visual Studio 會為專案中新的單一 SSIS 套件 (Package.dtsx) 開啟設計工具。 您會看到下列畫面區域：

* 左側是 SSIS 元件的 [工具箱]。
* 中間是有許多索引標籤的設計介面。 一般來說，您至少會使用 [控制流程] 和 [資料流程] 索引標籤。
* 右側是 [方案總管] 和 [屬性] 窗格。
  
    ![][01]

## <a name="step-2-create-the-basic-data-flow"></a>步驟 2：建立基本資料流程
1. 將 [資料流程工作] 從 [工具箱] 拖曳至設計介面的中央 (在 [控制流程] 索引標籤上)。
   
    ![][02]
2. 按兩下 [資料流程工作] 以切換到 [資料流程] 索引標籤。
3. 從 [工具箱] 的 [其他來源] 清單中，將 [ADO.NET 來源] 拖曳至設計介面。 保持選取來源配接器，在 [屬性] 窗格中將其名稱變更為 **SQL Server 來源**。
4. 從 [工具箱] 的 [其他目的地] 清單中，將 [ADO.NET 目的地] 拖曳至設計介面的 [ADO.NET 來源] 底下。 保持選取目的地配接器，在 [屬性] 窗格中將其名稱變更為 **SQL DW 目的地**。
   
    ![][09]

## <a name="step-3-configure-the-source-adapter"></a>步驟 3：設定來源配接器
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

## <a name="step-4-connect-the-source-adapter-to-the-destination-adapter"></a>步驟 4：將來源配接器連線到目的地配接器
1. 在設計介面上選取來源配接器。
2. 選取從來源配接器延伸的藍色箭頭，並將它拖曳到目的地編輯器，直到它貼齊固定。
   
    ![][10]
   
    在一般的 SSIS 套件中，您可以在來源和目的地之間使用 SSIS 工具箱中的數個其他元件，以在資料通過 SSIS 資料流程時進行架構重組、轉換和清理。 為了盡可能使此範例簡單，我們會將來源直接連線到目的地。

## <a name="step-5-configure-the-destination-adapter"></a>步驟 5：設定目的地配接器
1. 按兩下目的地配接器以開啟 [ADO.NET 目的地編輯器]。
   
    ![][11]
2. 在 [ADO.NET 目的地編輯器] 的 [連線管理員] 索引標籤上，按一下 [連線管理員] 清單旁的 [新增] 按鈕，以開啟 [設定 ADO.NET 連線管理員] 對話方塊，然後針對本教學課程載入資料的目的地 Azure SQL 資料倉儲資料庫建立連線設定。
3. 在 [設定 ADO.NET 連線管理員] 對話方塊中，按一下 [新增] 按鈕以開啟 [連線管理員] 對話方塊並建立新的資料連線。
4. 在 [連線管理員] 對話方塊中，執行下列事項。
   1. 針對 [提供者]，選取 [SqlClient 資料提供者]。
   2. 針對 [伺服器名稱]，輸入 SQL 資料庫倉儲名稱。
   3. 在 [登入伺服器] 區段中，選取 [使用 SQL Server 驗證] 並輸入驗證資訊。
   4. 在 [連線到資料庫] 區段中，選取現有的 SQL 資料倉儲資料庫。
   5. 按一下 **[測試連接]**。
   6. 在報告連線測試結果的對話方塊中，按一下 [確定] 以返回 [連線管理員] 對話方塊。
   7. 在 [連線管理員] 對話方塊中，按一下 [確定] 以返回 [設定 ADO.NET 連線管理員] 對話方塊。
5. 在 [設定 ADO.NET 連線管理員] 對話方塊中，按一下 [確定] 以返回 [ADO.NET 目的地編輯器]。
6. 在 [ADO.NET 目的地編輯器] 中，按一下 [使用資料表或檢視] 清單旁的 [新增] 以開啟 [建立資料表] 對話方塊，並使用與來源資料表相符的資料行清單建立新的目的地資料表。
   
    ![][12a]
7. 在 [建立資料表] 對話方塊中，執行下列事項。
   
   1. 將目的地資料表的名稱變更為 **SalesOrderDetail**。
   2. 移除 **rowguid** 資料行。 SQL 資料倉儲中不支援 **uniqueidentifier** 資料類型。
   3. 將 **LineTotal** 資料行的資料類型變更為 **money**。 SQL 資料倉儲中不支援 **decimal** 資料類型。 如需支援資料類型的詳細資訊，請參閱 [CREATE TABLE (Azure SQL 資料倉儲、平行處理資料倉儲)][CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]。
      
       ![][12b]
   4. 按一下 [確定] 以建立資料表，並返回 [ADO.NET 目的地編輯器]。
8. 在 [ADO.NET 目的地編輯器] 中，選取 [對應] 索引標籤以查看來源中的資料行如何對應至目的地中的資料行。
   
    ![][13]
9. 按一下 [確定] 以完成設定資料來源。

## <a name="step-6-run-the-package-to-load-the-data"></a>步驟 6：執行套件以載入資料
按一下工具列上的 [啟動] 按鈕，或選取 [偵錯] 功能表上的其中一個 [執行] 選項來執行套件。

當套件開始執行時，您會看到黃色旋轉的轉輪表示活動，以及目前為止所處理的資料列數目。

![][14]

當套件完成執行時，您會看到綠色核取記號表示已成功，以及從來源載入至目的地的資料列總數。

![][15]

恭喜！ 您已成功地使用 SQL Server Integration Services 將資料載入至 Azure SQL 資料倉儲。

## <a name="next-steps"></a>後續步驟
* 深入了解 SSIS 資料流程。 從這裡開始：[資料流程][Data Flow]。
* 了解如何直接在設計環境中針對您的套件進行偵錯及疑難排解。 從這裡開始：[套件開發的疑難排解工具][Troubleshooting Tools for Package Development]。
* 了解如何將您的 SSIS 專案和套件部署到 Integration Services 伺服器或另一個儲存位置。 從這裡開始：[部署專案和套件][Deployment of Projects and Packages]。

<!-- Image references -->
[01]:  ./media/load-data-to-sql-data-warehouse/ssis-designer-01.png
[02]:  ./media/load-data-to-sql-data-warehouse/ssis-data-flow-task-02.png
[03]:  ./media/load-data-to-sql-data-warehouse/ado-net-source-03.png
[04]:  ./media/load-data-to-sql-data-warehouse/ado-net-connection-manager-04.png
[05]:  ./media/load-data-to-sql-data-warehouse/ado-net-connection-05.png
[06]:  ./media/load-data-to-sql-data-warehouse/test-connection-06.png
[07]:  ./media/load-data-to-sql-data-warehouse/ado-net-source-07.png
[08]:  ./media/load-data-to-sql-data-warehouse/preview-data-08.png
[09]:  ./media/load-data-to-sql-data-warehouse/source-destination-09.png
[10]:  ./media/load-data-to-sql-data-warehouse/connect-source-destination-10.png
[11]:  ./media/load-data-to-sql-data-warehouse/ado-net-destination-11.png
[12a]: ./media/load-data-to-sql-data-warehouse/destination-query-before-12a.png
[12b]: ./media/load-data-to-sql-data-warehouse/destination-query-after-12b.png
[13]:  ./media/load-data-to-sql-data-warehouse/column-mapping-13.png
[14]:  ./media/load-data-to-sql-data-warehouse/package-running-14.png
[15]:  ./media/load-data-to-sql-data-warehouse/package-success-15.png

<!-- Article references -->

<!-- MSDN references -->
[PolyBase Guide]: ../relational-databases/polybase/polybase-guide.md
[Download SQL Server Data Tools (SSDT)]: ../ssdt/download-sql-server-data-tools-ssdt.md
[CREATE TABLE (Azure SQL Data Warehouse, Parallel Data Warehouse)]: ../t-sql/statements/create-table-azure-sql-data-warehouse.md
[Data Flow]: ./data-flow/data-flow.md
[Troubleshooting Tools for Package Development]: ./troubleshooting/troubleshooting-tools-for-package-development.md
[Deployment of Projects and Packages]: ./packages/deploy-integration-services-ssis-projects-and-packages.md

<!--Other Web references-->
[Microsoft SQL Server 2016 Integration Services Feature Pack for Azure]: http://go.microsoft.com/fwlink/?LinkID=626967
[SQL Server Evaluations]: https://www.microsoft.com/evalcenter/evaluate-sql-server-2016
[Visual Studio Community]: https://www.visualstudio.com/products/visual-studio-community-vs.aspx
[AdventureWorks 2014 Sample Databases]: https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks
