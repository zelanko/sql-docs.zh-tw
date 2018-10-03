---
title: 第 8 課：建立資料篩選 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 19ccbdba-e3da-40a4-b652-32c628cf32e5
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: d5004ad7cb8283be11d7e89f96ee46bd29ccccd6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48189918"
---
# <a name="lesson-8-create-a-data-filter"></a>第 8 課：建立資料篩選
  在父報表上加入鑽研動作後，下一步是要針對您為子報表定義的資料表建立資料篩選。  
  
 您可以為鑽研報表建立以資料表為基礎的篩選， **或** 查詢篩選。 本課將提供這兩個選項的指示。  
  
## <a name="table-based-filter"></a>以資料表為基礎的篩選  
 您需要完成下列工作，才能實作以資料表為基礎的篩選。  
  
-   將篩選運算式加入至子報表中的 Tablix。  
  
-   建立從 `PurchaseOrderDetail` 資料表選取未篩選資料的函數。  
  
-   加入將 `PurchaseOrderDetail` DataTable 繫結至子報表的事件處理常式。  
  
#### <a name="to-add-a-filter-expression-to-the-tablix-in-the-child-report"></a>若要將篩選運算式加入至子報表中的 Tablix  
  
1.  開啟子報表。  
  
2.  選取 tablix 中的資料行標題，以滑鼠右鍵按一下資料行標題，上方出現的灰色資料格，然後按一下**Tablix 屬性**。  
  
3.  按一下 **篩選條件**頁面，然後再按一下**新增**。  
  
4.  在 **運算式**欄位中，按一下 `ProductID`從下拉式清單。 這是要套用篩選的資料行。  
  
5.  按一下 等於 (**=**) 中的運算子**運算子**下拉式清單。  
  
6.  旁按一下 [運算式] 按鈕**值**欄位中，按一下**參數**中**分類**區域中，然後再按兩下`productid`中**值**區域。 [設定運算式對象: 值] 欄位現在應該包含類似 **=Parameters!productid.Value** 的運算式。  
  
7.  按一下 [ **[確定]** 並 **[確定]** 中再次**Tablix 屬性**] 對話方塊。  
  
8.  儲存 .rdlc 檔。  
  
#### <a name="to-create-a-function-that-selects-unfiltered-data-from-the-purchaseordedetail-table"></a>若要建立從 PurchaseOrdeDetail 資料表選取未篩選資料的函數  
  
1.  在 [方案總管] 中展開 [Default.aspx]，然後按兩下 [Default.aspx.cs]。  
  
2.  建立接受整數類型參數 `productid` 且傳回 `datatable` 物件的新函數，並執行下列操作。  
  
    1.  建立資料集的執行個體`DataSet2`，步驟 2 中建立[第 4 課： 定義子報表的資料連接和資料表](lesson-4-define-a-data-connection-and-data-table-for-child-report.md)。  
  
    2.  建立與 SqlServer 資料庫的連接，以執行 **第 4 課：定義子報表的資料連接和資料表**中定義的查詢。  
  
    3.  查詢會傳回未篩選的資料。  
  
    4.  執行查詢可在 DataSet 執行個體中填入未篩選資料。  
  
    5.  傳回 `PurchaseOrderDetail` DataTable。  
  
         函數看起來類似下面所示 (僅供參考。 您可以依照想要的任何模式提取必要的子報表資料)。  
  
        ```  
        /// <summary>  
            /// Function to query PurchaseOrderDetail table, fetch the  
            /// unfiltered data and bind it with the Child report  
            /// </summary>  
            /// <returns>A dataTable of type PurchaseOrderDetail</returns>  
            private DataTable GetPurchaseOrderDetail()  
            {  
                try  
                {  
                    //Create the instance for the typed dataset, DataSet2 which will   
                    //hold the [PurchaseOrderDetail] table details.  
                    //The dataset was created as part of the tutorial in Step 4.  
                    DataSet2 ds = new DataSet2();  
  
                    //Create a SQL Connection to the AdventureWorks2008 database using Windows Authentication.  
                    using (SqlConnection sqlconn = new SqlConnection("Data Source=.;Initial Catalog=Adventureworks;Integrated Security=SSPI"))  
                    {  
                        //Building the dynamic query with the parameter ProductID.  
                        SqlDataAdapter adap = new SqlDataAdapter("SELECT PurchaseOrderID, PurchaseOrderDetailID, OrderQty, ProductID, ReceivedQty, RejectedQty, StockedQty FROM Purchasing.PurchaseOrderDetail ", sqlconn);  
                        //Executing the QUERY and fill the dataset with the PurchaseOrderDetail table data.  
                        adap.Fill(ds, "PurchaseOrderDetail");  
                    }  
  
                    //Return the PurchaseOrderDetail table for the Report Data Source.  
                    return ds.PurchaseOrderDetail;  
                }  
                catch  
                {  
                    throw;  
                }  
            }  
        ```  
  
#### <a name="to-add-an-event-handler-that-binds-the-purchaseorderdetail-datatable-to-the-child-report"></a>若要加入將 PurchaseOrderDetail DataTable 繫結至子報表的事件處理常式  
  
1.  開啟 [Default.aspx]。  
  
2.  以滑鼠右鍵按一下 ReportViewer 控制項中，然後再按一下**屬性。**  
  
3.  在 **屬性**頁面上，按一下**事件**圖示。  
  
4.  按兩下**鑽研**事件。  
  
     這樣會在程式碼中加入事件處理常式區段，看起來類似下面區塊。  
  
    ```  
    protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
    {  
    }  
    ```  
  
5.  完成事件處理常式。 它應該包含下列功能。  
  
    1.  從 *DrillthroughEventArgs* 參數提取子報表物件參考。  
  
    2.  呼叫函式， `GetPurchaseOrderDetail`  
  
    3.  將 `PurchaseOrderDetail` DataTable 與報表的對應資料來源繫結。  
  
         完成的事件處理常式程式碼看起來如下所示。  
  
        ```  
        protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
            {  
                try  
                {  
                     //Get the instance of the Target report, in our case the JumpReport.rdlc.  
                    LocalReport report = (LocalReport)e.Report;  
  
                     //Binding the DataTable to the Child report dataset.  
                    //The name DataSet1 which can be located from,   
                    //Go to Design view of Child.rdlc, Click View menu -> Report Data  
                    //You'll see this name under DataSet2.  
                    report.DataSources.Add(new ReportDataSource("DataSet1", GetPurchaseOrderDetail()));  
                }  
                catch (Exception ex)  
                {  
                    Response.Write(ex.Message);  
                }  
            }  
        ```  
  
6.  儲存檔案。  
  
## <a name="query-filter"></a>查詢篩選  
 您需要完成下列工作，才能實作查詢篩選。  
  
-   建立從 `PurchaseOrderDetail` 資料表選取已篩選資料的函數。  
  
-   加入擷取參數值並將 `PurchaseOrdeDetail` DataTable 繫結至子報表的事件處理常式。  
  
#### <a name="to-create-a-function-that-selects-filtered-data-from-the-purchaseorderdetail-table"></a>若要建立從 PurchaseOrderDetail 資料表選取已篩選資料的函數  
  
1.  在 [方案總管] 中展開 [Default.aspx]，然後按兩下 [Default.aspx.cs]。  
  
2.  建立接受整數類型參數 `productid` 且傳回 `datatable` 物件的新函數，並執行下列操作。  
  
    1.  建立資料集的執行個體`DataSet2`，步驟 2 中建立[第 4 課： 定義子報表的資料連接和資料表](lesson-4-define-a-data-connection-and-data-table-for-child-report.md)。  
  
    2.  建立與 SqlServer 資料庫的連接，以執行 **第 4 課：定義子報表的資料連接和資料表**中定義的查詢。  
  
    3.  查詢將包含參數 `productid`，確保傳回的資料是根據父報表中選取的 `ProductID` 篩選。  
  
    4.  執行查詢可在 DataSet 執行個體中填入已篩選資料。  
  
    5.  傳回 `PurchaseOrderDetail` DataTable。  
  
         函數看起來類似下面所示 (僅供參考。 您可以依照想要的任何模式提取必要的子報表資料)。  
  
        ```  
        /// <summary>  
            /// Function to query PurchaseOrderDetail table and filter the  
            /// data for a specific ProductID selected in the Parent report.  
            /// </summary>  
            /// <param name="productid">Parameter passed from the Parent report to filter data.</param>  
            /// <returns>A dataTable of type PurchaseOrderDetail</returns>  
            private DataTable GetPurchaseOrderDetail(int productid)  
            {  
                try  
                {  
                    //Create the instance for the typed dataset, DataSet2 which will   
                    //hold the [PurchaseOrderDetail] table details.  
                    //The dataset was created as part of the tutorial in Step 4.  
                    DataSet2 ds = new DataSet2();  
  
                    //Create a SQL Connection to the AdventureWorks2008 database using Windows Authentication.  
                    using (SqlConnection sqlconn = new SqlConnection("Data Source=.;Initial Catalog=Adventureworks;Integrated Security=SSPI"))  
                    {  
                        //Building the dynamic query with the parameter ProductID.  
                        SqlDataAdapter adap = new SqlDataAdapter("SELECT PurchaseOrderID, PurchaseOrderDetailID, OrderQty, ProductID, ReceivedQty, RejectedQty, StockedQty FROM Purchasing.PurchaseOrderDetail where ProductID = " + productid, sqlconn);  
                        //Executing the QUERY and fill the dataset with the PurchaseOrderDetail table data.  
                        adap.Fill(ds, "PurchaseOrderDetail");  
                    }  
  
                    //Return the PurchaseOrderDetail table for the Report Data Source.  
                    return ds.PurchaseOrderDetail;  
                }  
                catch  
                {  
                    throw;  
                }  
            }  
        ```  
  
#### <a name="to-add-an-event-handler-that-retrieves-parameter-values-and-binds-the-purchaseordedetail-datatable-to-the-child-report"></a>若要加入擷取參數值並將 PurchaseOrdeDetail DataTable 繫結至子報表的事件處理常式  
  
1.  開啟 [Default.aspx]。  
  
2.  ReportViewer 控制項中，以滑鼠右鍵按一下，然後按一下**屬性**。  
  
3.  在 **屬性**窗格中，按一下**事件**圖示。  
  
4.  按兩下**鑽研**事件。  
  
     這樣會在程式碼中加入事件處理常式區段，看起來類似下面所示。  
  
    ```  
    protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
    {  
    }  
    ```  
  
5.  完成事件處理常式。 它應該包含下列功能。  
  
    1.  從 *DrillthroughEventArgs* 參數提取子報表物件參考。  
  
    2.  從提取的子報表物件取得子報表參數清單。  
  
    3.  反覆運算參數集合，並擷取從父報表傳遞之參數 `ProductID` 的值。  
  
    4.  呼叫函數 `GetPurchaseOrderDetail`，並傳遞參數 `ProductID` 的值。  
  
    5.  將 `PurchaseOrderDetail` DataTable 與報表的對應資料來源繫結。  
  
         完成的事件處理常式程式碼看起來如下所示。  
  
        ```  
        protected void ReportViewer1_Drillthrough(object sender, Microsoft.Reporting.WebForms.DrillthroughEventArgs e)  
            {  
                try  
                {  
                    //Variable to store the parameter value passed from the MainReport.  
                    int productid = 0;  
  
                    //Get the instance of the Target report, in our case the JumpReport.rdlc.  
                    LocalReport report = (LocalReport)e.Report;  
  
                    //Get all the parameters passed from the main report to the target report.  
                    //OriginalParametersToDrillthrough actually returns a Generic list of   
                    //type ReportParameter.  
                    IList<ReportParameter> list = report.OriginalParametersToDrillthrough;  
  
                    //Parse through each parameters to fetch the values passed along with them.  
                    foreach (ReportParameter param in list)  
                    {  
                        //Since we know the report has only one parameter and it is not a multivalued,   
                        //we can directly fetch the first value from the Values array.  
                        productid = Convert.ToInt32(param.Values[0].ToString());  
                    }  
  
                    //Binding the DataTable to the Child report dataset.  
                    //The name DataSet1 which can be located from,   
                    //Go to Design view of Child.rdlc, Click View menu -> Report Data  
                    //You'll see this name under DataSet2.  
                    report.DataSources.Add(new ReportDataSource("DataSet1", GetPurchaseOrderDetail(productid)));  
                }  
                catch (Exception ex)  
                {  
                    Response.Write(ex.Message);  
                }  
            }  
        ```  
  
6.  儲存檔案。  
  
## <a name="next-task"></a>下一項工作  
 您已成功針對您為子報表定義的資料表建立資料篩選。 接下來您將建立並執行網站應用程式。  
  
  
