---
title: "第 2 課： 定義父報表的資料連接和資料表 |Microsoft 文件"
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: f02dee0c-85ad-45d4-b707-10e9e8541db9
caps.latest.revision: 8
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: adc2cc7d329586bae6fb85edb08d71fe51aaaef8
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="lesson-2-define-a-data-connection-and-data-table-for-parent-report"></a>第 2 課：定義父報表的資料連接和資料表
使用 Visual C# 的 ASP.NET 網站範本建立新的網站專案後，下一步是要建立父報表的資料連接和資料表。 在本教學課程中，資料連接是指 AdventureWorks2014 資料庫。  
  
## <a name="to-define-a-data-connection-and-data-table-by-adding-a-dataset-for-parent-report"></a>若要藉由加入 DataSet 定義資料連接和資料表 (針對父報表)  
  
1.  在**網站**功能表上，選取**加入新項目**。  
  
2.  在**加入新項目**對話方塊中，選取**資料集**選取**新增**。 出現提示時您應該將項目加入**App_Code**資料夾選取**是**。  
  
    這樣會將新的 XSD 檔 **DataSet1.xsd** 新增至專案，並開啟 DataSet 設計工具。  
  
3.  從 [工具箱] 視窗將 **[TableAdapter](http://msdn.microsoft.com/library/bz9tthwx.aspx)** 控制項拖曳至設計介面。 這樣會啟動 [ **TableAdapter** 組態精靈]。  
  
4.  在**選擇資料連接**頁面上，選取**新連線**。  
  
5.  如果這是第一次的資料來源中建立 Visual Studio 中，您會看到**選擇資料來源**頁面。 在**資料來源**方塊中，選取**Microsoft SQL Server**。  
  
6.  在**加入連接**對話方塊方塊中，執行下列步驟：  
  
    1.  在**伺服器名稱**方塊中，輸入伺服器位置**AdventureWorks2014**所在的資料庫。  
  
        預設的 SQL Server Express 執行個體為 **(local)\sqlexpress**。  
  
    2.  在**登入伺服器**區段中，選取的選項，可讓您存取資料。 **使用 Windows 驗證**是預設值。  
  
    3.  從**選取或輸入資料庫名稱**下拉式清單中選取**AdventureWorks2014**。  
  
    4.  依序選取 [確定] 和 [下一步]。  
  
7.  如果您選取**使用 SQL Server 驗證**在步驟 6 (b) 中，選擇要在字串中包含敏感性資料還是在應用程式程式碼中設定的資訊。  
  
8.  在**連接字串儲存到應用程式組態檔**頁面上，輸入連接字串的名稱或接受預設值**AdventureWorks2014ConnectionString**。 選取 **[下一步]**。  
  
9. 在**選擇命令類型**頁面上，選取**使用 SQL 陳述式**，然後選取**下一步**。  
  
10. 在**輸入 SQL 陳述式**頁面上，輸入下列 TRANSACT-SQL 查詢，以從中擷取資料**AdventureWorks2014**資料庫，然後再選取**下一步**。  
  
    ```  
    SELECT ProductID, Name, ProductNumber, SafetyStockLevel, ReorderPoint FROM  Production.Product Order By ProductID  
    ```  
  
    您也可以建立查詢，藉由選取**查詢產生器**，然後選取驗證查詢**執行查詢**。 如果查詢未傳回預期的資料，表示您可能使用較舊的 AdventureWorks 版本。 如需如何取得 **AdventureWorks2014** 範例資料庫的詳細資訊，請參閱 [Microsoft SQL Server 資料庫產品範例](http://msftdbprodsamples.codeplex.com/)。  
  
11. 在**選擇要產生的方法**頁面上，請務必取消核取**建立方法，以將更新傳送至資料庫 (GenerateDBDirectMethods) 直接**，然後選取**完成**。  
  
    > [!WARNING]  
    > 務必取消核取**建立方法，以更新直接傳送到資料庫 (GenerateDBDirectMethods)**  
  
    現在您已完成設定 ADO.NET DataTable 物件做為報表的資料來源。 在 Visual Studio 中的 DataSet 設計工具頁面上，應該會看到您加入的 DataTable 物件，並且列出查詢中指定的資料行。 根據查詢，DataSet1 包含 Product 資料表中的資料。  
  
12. 儲存檔案。  
  
13. 若要預覽資料，請選取**預覽資料**上**資料** 功能表，然後選取**預覽**。  
  
## <a name="next-task"></a>下一項工作  
您已成功建立父報表的資料連接和資料表。 接下來您將使用 [報表精靈] 設計父報表。 請參閱 [第 3 課：使用報表精靈設計父報表](../reporting-services/lesson-3-design-the-parent-report-using-the-report-wizard.md)。  
  


