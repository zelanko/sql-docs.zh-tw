---
title: 第 2 課：定義父報表的資料連線和資料表 | Microsoft Docs
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: f02dee0c-85ad-45d4-b707-10e9e8541db9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: dfdddd3e263ef6f83f8ad12635c76c61fef6e284
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47603124"
---
# <a name="lesson-2-define-a-data-connection-and-data-table-for-parent-report"></a>第 2 課：定義父報表的資料連接和資料表
使用 Visual C# 的 ASP.NET 網站範本建立新的網站專案後，下一步是要建立父報表的資料連接和資料表。 在本教學課程中，資料連接是指 AdventureWorks2014 資料庫。  
  
## <a name="to-define-a-data-connection-and-data-table-by-adding-a-dataset-for-parent-report"></a>若要藉由加入 DataSet 定義資料連接和資料表 (針對父報表)  
  
1.  在 [網站] 功能表上選取 [新增項目]。  
  
2.  在 [新增項目] 對話方塊中，選取 [資料集]，然後選取 [新增]。 出現提示時，您應該選取 [是]，將項目新增至 **App_Code** 資料夾。  
  
    這樣會將新的 XSD 檔 **DataSet1.xsd** 新增至專案，並開啟 DataSet 設計工具。  
  
3.  從 [工具箱] 視窗將 **[TableAdapter](http://msdn.microsoft.com/library/bz9tthwx.aspx)** 控制項拖曳至設計介面。 這樣會啟動 [ **TableAdapter** 組態精靈]。  
  
4.  在 [選擇資料連接] 頁面上，選取 [新增連接]。  
  
5.  如果您是第一次在 Visual Studio 中建立資料來源，則會看見 [選擇資料來源] 頁面。 在 [資料來源] 方塊中，選取 [Microsoft SQL Server]。  
  
6.  在 [新增連線] 對話方塊中，執行下列步驟：  
  
    1.  在 [伺服器名稱] 方塊中，輸入 **AdventureWorks2014** 資料庫所在的伺服器。  
  
        預設的 SQL Server Express 執行個體為 **(local)\sqlexpress**。  
  
    2.  在 [登入伺服器] 區段中，選取提供資料存取的選項。 [使用 Windows 驗證] 是預設值。  
  
    3.  從 [選取或輸入資料庫名稱] 下拉式清單中，選取 [AdventureWorks2014]。  
  
    4.  依序選取 [確定] 和 [下一步]。  
  
7.  如果您已在步驟 6 (b) 中選取 [使用 SQL Server 驗證]，請選取在字串中包含敏感性資料或在應用程式程式碼中設定資訊的選項。  
  
8.  在 [將連接字串儲存到應用程式設定檔] 頁面上，鍵入連接字串的名稱，或接受預設 **AdventureWorks2014ConnectionString**。 選取 **[下一步]**。  
  
9. 在 [選擇命令類型] 頁面上，選取 [使用 SQL 陳述式]，然後選取 [下一步]。  
  
10. 在 [輸入 SQL 陳述式] 頁面上，輸入下列 Transact-SQL 查詢，以便從 **AdventureWorks2014** 資料庫擷取資料，然後選取 [下一步]。  
  
    ```  
    SELECT ProductID, Name, ProductNumber, SafetyStockLevel, ReorderPoint FROM  Production.Product Order By ProductID  
    ```  
  
    您也可以選取 [查詢產生器] 建立查詢，然後選取 [執行查詢] 驗證查詢。 如果查詢未傳回預期的資料，表示您可能使用較舊的 AdventureWorks 版本。 如需如何取得 **AdventureWorks2014** 範例資料庫的詳細資訊，請參閱 [AdventureWorks 範例資料庫](https://github.com/Microsoft/sql-server-samples/releases)。  
  
11. 務必在 [選擇要產生的方法] 頁面上取消核取 [建立方法以直接將更新傳送至資料庫 (GenerateDBDirectMethods)]，然後選取 [完成]。  
  
    > [!WARNING]  
    > 務必取消核取 [建立方法以直接將更新傳送至資料庫 (GenerateDBDirectMethods)]  
  
    現在您已完成設定 ADO.NET DataTable 物件做為報表的資料來源。 在 Visual Studio 中的 DataSet 設計工具頁面上，應該會看到您加入的 DataTable 物件，並且列出查詢中指定的資料行。 根據查詢，DataSet1 包含 Product 資料表中的資料。  
  
12. 儲存檔案。  
  
13. 若要預覽資料，請選取 [資料] 功能表上的 [預覽資料]，然後選取 [預覽]。  
  
## <a name="next-task"></a>下一項工作  
您已成功建立父報表的資料連接和資料表。 接下來您將使用 [報表精靈] 設計父報表。 請參閱 [第 3 課：使用報表精靈設計父報表](../reporting-services/lesson-3-design-the-parent-report-using-the-report-wizard.md)。  
  

