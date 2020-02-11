---
title: 第 4 課：定義子報表的資料連線和資料表 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a6aa2c56-227c-43c5-a28e-c7104131ac5e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c1008202519f1d9bcbf48dfdc4cd4ef3a3cbbe20
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108469"
---
# <a name="lesson-4-define-a-data-connection-and-data-table-for-child-report"></a>第 4 課：定義子報表的資料連接和資料表
  設計父報表之後，下一步是要建立子報表的資料連接和資料表。 在本教學課程中，資料連接是指 AdventureWorks2008 資料庫。 您也可以選擇連接到 AdventureWorks2012 資料庫。  
  
### <a name="to-define-a-data-connection-and-datatable-by-adding-a-dataset-for-child-report"></a>若要藉由加入 DataSet 定義資料連接和 DataTable (針對子報表)  
  
1.  在 [**網站**] 功能表上，按一下 [**加入新專案**]。  
  
2.  在 [**加入新專案**] 對話方塊中，按一下 [**資料集**]，然後按一下 [**加入**]。 出現提示時，您應該按一下 [**是]**，將專案新增至 [ **App_Code** ] 資料夾。  
  
     這樣會將新的 XSD 檔 **DataSet2.xsd** 加入專案，並開啟 DataSet 設計工具。  
  
3.  從 [工具箱] 視窗將 **TableAdapter** 控制項拖曳至設計介面。 這樣會啟動 [ **TableAdapter** 組態精靈]。  
  
4.  在 [**選擇您的資料連線**] 頁面上，按一下 [**新增連接**]。  
  
5.  在 [新增連線]  對話方塊中，執行下列步驟：  
  
    1.  在 [**伺服器名稱**] 方塊中，輸入**AdventureWorks2008**資料庫所在的伺服器。  
  
         預設的 SQL Server Express 執行個體為 **(local)\sqlexpress**。  
  
    2.  在 [登入伺服器]  區段中，選取提供資料存取的選項。 [使用 Windows 驗證]  是預設值。  
  
    3.  從 [**選取或輸入資料庫名稱**] 下拉式清單中，按一下 [ **AdventureWorks2008**]。  
  
    4.  按一下 [確定]****，然後按 [下一步]****。  
  
6.  如果您已在步驟 5 (b) 中選取 [使用 SQL Server 驗證]  ，請選取在字串中包含機密資料或在應用程式程式碼中設定資訊的選項。  
  
7.  在 [將**連接字串儲存到應用程式佈建檔**] 頁面上，輸入連接字串的名稱或接受預設**AdventureWorks2008ConnectionString**。 按 [下一步]  。  
  
8.  在 [**選擇命令類型**] 頁面上，選取 [**使用 SQL 語句]**，然後按 **[下一步**]。  
  
9. 在 [**輸入 SQL 語句**] 頁面上，輸入下列 transact-SQL 查詢以從**AdventureWorks2008**資料庫中取出資料，然後按 **[下一步]**。  
  
    ```  
    SELECT PurchaseOrderID, PurchaseOrderDetailID, OrderQty, ProductID, ReceivedQty, RejectedQty, StockedQty FROM Purchasing.PurchaseOrderDetail  
    ```  
  
     您也可以按一下 [**查詢**產生器] 來建立查詢，然後按一下 [**執行查詢**] 按鈕來驗證查詢。 如果查詢未傳回預期的資料，表示您可能使用較舊的 AdventureWorks 版本。 如需安裝**AdventureWorks2008**版本之 adventureworks 的詳細資訊，請參閱[逐步解說：安裝 adventureworks 資料庫](https://msdn.microsoft.com/library/aa992075\(v=vs.100\).aspx)。  
  
10. 在 [**選擇要產生的方法**] 頁面上，取消核取 [**建立方法以直接將更新傳送至資料庫（GenerateDBDirectMethods）**]，然後按一下 **[完成]**。  
  
     您現在已完成將 ADO.NET [DataTable](https://msdn.microsoft.com/library/system.data.datatable\(v=vs.100\).aspx)設定為報表的資料來源。 在 Visual Studio 中的 DataSet 設計工具頁面上，應該會看到您加入的 **DataTable** ，並且列出查詢中指定的資料行。 根據查詢，DataSet2 包含 PurhcaseOrderDetail 資料表中的資料。  
  
11. 儲存檔案。  
  
12. 若要預覽資料，請按一下 [**資料**] 功能表上的 [**預覽資料**]，然後按一下 [**預覽**]。  
  
## <a name="next-task"></a>下一項工作  
 您已成功建立子報表的資料連接和資料表。 接下來您將使用 [報表精靈] 設計子報表。  
  
  
