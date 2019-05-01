---
title: 第 2 課：修改報表資料來源屬性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: c962b0ff-ce8a-4742-8262-dc730901afcf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 41746f2938afd17e59dc4a9f2278179e4ccc1695
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63225158"
---
# <a name="lesson-2-modifying-the-report-data-source-properties"></a>第 2 課：修改報表資料來源屬性
  在這一課，您將使用報表管理員來選取傳遞給收件者的報表。 您將定義的資料驅動訂閱將散發 **建立基本資料表報表 &#40;SSRS 教學課程&#41;** 教學課程中建立的 [建立基本資料表報表 &amp;#40;SSRS 教學課程&amp;#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)報表。 在下面的步驟中，您將修改報表用來取得資料的資料來源連接資訊。 只有使用 **預存認證** 來存取報表資料來源的報表可以透過資料驅動訂閱散發。 自動報表處理需要預存認證。  
  
 您也會將資料集和報表修改成使用參數來依據 `[Order]` 篩選報表，讓訂閱能夠針對特定訂單和轉譯格式輸出不同的報表執行個體。  
  
 **本主題內容：**  
  
-   [若要修改的資料來源屬性](#bkmk_modify_datasource)  
  
-   [若要修改 AdventureWorksDataset](#bkmk_modify_dataset)  
  
-   [若要加入報表參數並重新發行報表](#bkmk_add_reportparameter)  
  
-   [若要重新部署報表](#bkmk_redeploy)  
  
##  <a name="bkmk_modify_datasource"></a> 若要修改的資料來源屬性  
  
1.  開始[報表管理員 &#40;SSRS 原生模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)系統管理員權限，例如，以滑鼠右鍵按一下 Internet explorer 的圖示，然後按一下**系統管理員身分執行**。  
  
2.  瀏覽到包含 **Sales Orders** 報表的資料夾，然後在報表的內容功能表中，按一下 **[管理]**。  
  
     ![開啟 [報表] 內容功能表，然後選取 [管理]](../../2014/tutorials/media/ssrs-tutorial-datadriven-manage-report.gif "開啟報表] 內容功能表，然後選取 [管理]")  
  
3.  按一下 [資料來源] 索引標籤。  
  
4.  針對 **[連接類型]**，選取 **[Microsoft SQL Server]**。  
  
5.  自訂資料來源連接字串將如下所示，而且它會假設範例資料庫位於本機資料庫伺服器上：  
  
    ```  
    Data source=localhost; initial catalog=AdventureWorks2012  
    ```  
  
6.  按一下 **[安全地儲存在報表伺服器中的認證]**。  
  
7.  輸入您的使用者名稱 (使用 *domain\user*格式) 和密碼。 如果您沒有存取權限[!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]資料庫，請指定登入。  
  
8.  按一下 **當做 windows 認證連接到資料來源時使用**，然後按一下**確定**。 如果您不想要使用網域帳戶 (例如，如果您使用[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]登入)，請不要按此核取方塊。  
  
9. 按一下 [測試連接]，確認您能夠連線到資料來源。  
  
10. 按一下 **[套用]**。  
  
11. 檢視報表以確認報表是以您指定的認證來執行。 若要檢視報表，請按一下 [ **檢視** ] 索引標籤。請注意，報表開啟之後，您必須選取員工姓名，然後按一下**檢視報表**按鈕，以檢視報表。  
  
##  <a name="bkmk_modify_dataset"></a> 若要修改 AdventureWorksDataset  
  
1.  銷售訂單中開啟報表 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]  
  
2.  以滑鼠右鍵按一下 `AdventureWorksDataset` 資料集，然後按一下 [資料集屬性]。  
  
3.  在 `WHERE (UPPER(SalesOrderNumber) =UPPER(@OrderNumber) or  @OrderNumber IS NULL)` 陳述式前面加入 `Group By` 陳述式。 完整的查詢語法如下：  
  
    ```  
    SELECT soh.OrderDate AS Date, soh.SalesOrderNumber AS [Order], pps.Name AS Subcat, pp.Name AS Product, SUM(sd.OrderQty) AS Qty, SUM(sd.LineTotal)  AS LineTotal  
    FROM Sales.SalesPerson AS sp INNER JOIN  
      Sales.SalesOrderHeader AS soh ON sp.BusinessEntityID = soh.SalesPersonID INNER JOIN  
       Sales.SalesOrderDetail AS sd ON sd.SalesOrderID = soh.SalesOrderID INNER JOIN  
       Production.Product AS pp ON sd.ProductID = pp.ProductID  
    INNER JOIN  
       Production.ProductSubcategory AS pps ON pp.ProductSubcategoryID = pps.ProductSubcategoryID   
    INNER JOIN  
        Production.ProductCategory AS ppc ON ppc.ProductCategoryID = pps.ProductCategoryID  
  
    WHERE (UPPER(SalesOrderNumber) =UPPER(@OrderNumber) or  @OrderNumber IS NULL)  
  
    GROUP BY ppc.Name, soh.OrderDate, soh.SalesOrderNumber, pps.Name, pp.Name, soh.SalesPersonID  
    HAVING (ppc.Name = 'Clothing')  
    ```  
  
4.  按一下 **[確定]**。  
  
##  <a name="bkmk_add_reportparameter"></a> 若要加入報表參數並重新發行報表  
  
1.  在 **報表資料**窗格中，按一下**新增**，然後按一下 **參數...**  
  
2.  在 **[名稱]** 中，輸入 `OrderNumber`。  
  
3.  在 **[提示]** 中，輸入 `OrderNumber`。  
  
4.  選取 [允許空白值 ("")]。  
  
5.  選取 [允許 Null 值]。  
  
6.  按一下 [確定] 。 參數會加入至**報表資料 窗格**和它看起來如下圖所示：  
  
     ![新的參數加入至 [報表資料] 窗格](../../2014/tutorials/media/ssrs-tutorial-datadriven-parameter.gif "新的參數加入至 [報表資料] 窗格")  
  
7.  按一下 [**預覽**來執行報表] 索引標籤。請注意，在報表頂端的參數輸入的方塊。 您可以：  
  
    -   按一下 [檢視報表] 查看完整報表，而不使用參數。  
  
    -   取消選取 Null 選項並輸入訂單號碼 (例如 so71949)，即可單獨檢視報表中的單一訂單。  
  
         ![具有可見參數區域的報表檢視器](../../2014/tutorials/media/ssrs-tutorial-datadriven-reportviewer-parameter.gif "具有可見參數區域的報表檢視器")  
  
8.  請重新部署報表，讓下一課的訂閱組態能夠運用您在這一課所做的變更。 如需有關用於資料表教學課程中的專案屬性的詳細資訊，請參閱 ' 若要將報表發行至報表伺服器 （選擇性）' 區段的[第 6 課：加入群組和總計&#40;Reporting Services&#41;](../reporting-services/lesson-6-adding-grouping-and-totals-reporting-services.md)。  
  
##  <a name="bkmk_redeploy"></a> 若要重新部署報表  
  
1.  請重新部署報表，讓下一課的訂閱組態能夠運用您在這一課所做的變更。 如需有關用於資料表教學課程中的專案屬性的詳細資訊，請參閱 ' 若要將報表發行至報表伺服器 （選擇性）' 區段的[第 6 課：加入群組和總計&#40;Reporting Services&#41;](../reporting-services/lesson-6-adding-grouping-and-totals-reporting-services.md)。  
  
2.  在工具列上，按一下 **[建置]** ，然後按一下 **[部署教學課程]**。  
  
## <a name="next-steps"></a>後續步驟  
 您已順利設定報表來利用預存認證取得資料。 之後，您可以使用報表管理員中的 [資料驅動訂閱] 頁面來指定訂閱。 請參閱[第 3 課：定義資料驅動訂閱](../reporting-services/lesson-3-defining-a-data-driven-subscription.md)。  
  
## <a name="see-also"></a>另請參閱  
 [管理報表資料來源](report-data/manage-report-data-sources.md)   
 [指定報表資料來源的認證及連接資訊](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [建立資料驅動訂閱 &#40;SSRS 教學課程&#41;](../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)   
 [建立基本資料表報表 &#40;SSRS 教學課程&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  
  
  
