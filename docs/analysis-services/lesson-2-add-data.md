---
title: "第 2 課： 將資料加入 |Microsoft 文件"
ms.custom: 
ms.date: 06/19/2017
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
ms.assetid: 13c3a8cc-b1db-4aba-ad9b-038b7971be8d
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: efd2e0c85d8c266050e74d5c363afe33e37c48c1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="lesson-2-add-data"></a>第 2 課：加入資料
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

在這一課，您將使用 「 資料表匯入精靈 」 在 SSDT 中連接 AdventureWorksDW SQL 範例資料庫，選取資料、 預覽和篩選資料，然後將資料匯入您的模型工作空間。  
  
使用 [資料表匯入精靈] 可讓您從各種關聯式來源匯入資料：Access、SQL、Oracle、Sybase、Informix、DB2、Teradata 以及其他來源。 從每一個關聯式來源匯入資料的步驟非常類似以下所述內容。 資料也可以選取使用預存程序。 若要了解有關匯入資料，您可以從匯入的資料來源的不同類型的詳細資訊，請參閱[資料來源](../analysis-services/tabular-models/data-sources-ssas-tabular.md)。  
  
完成本課程的估計時間： **20 分鐘**  
  
## <a name="prerequisites"></a>必要條件  
本主題是表格式模型教學課程的一部分，必須依序完成。 在執行本課程的工作之前，您應已完成上一課： [第 1 課：建立新的表格式模型專案](../analysis-services/lesson-1-create-a-new-tabular-model-project.md)。  
  
## <a name="create-a-connection"></a>建立連接  
  
#### <a name="to-create-a-connection-to-a-the-adventureworksdw2014-database"></a>若要建立的連接 AdventureWorksDW2014 資料庫  
  
1.  在表格式模型總管 中，以滑鼠右鍵按一下**資料來源** > **從資料來源匯入**。  
  
    這會啟動 [資料表匯入精靈] 會引導您完成設定資料來源的連接。 如果您沒有看到表格式模型總管，按兩下  **Model.bim**中**方案總管 中**在設計師中開啟模型。 
    
    ![做為表格式-第 2 課-所時間](../analysis-services/media/as-tabular-lesson2-tme.png) 

    注意： 如果您正在建立您的模型 1400年相容性層級，您會看到新的 [取得資料] 功能而不是 「 資料表匯入精靈 」。 對話方塊會顯示從下列步驟稍有不同，但是您仍然可以要跟著做。 
  
2.  在 資料表匯入精靈，在**關聯式資料庫**，按一下**Microsoft SQL Server** > **下一步**。  
  
3.  在 [連接到 Microsoft SQL Server 資料庫] 頁面的 [易記連接名稱] 中，輸入 **Adventure Works DB from SQL**。  
  
4.  在**伺服器名稱**，輸入您安裝 AdventureWorksDW 資料庫的伺服器名稱。  
  
5.  在**資料庫名稱**欄位中，選取**AdventureWorksDW**，然後按一下 **下一步**。  
  
    ![為-表格式-第 2 課-tiw-名稱](../analysis-services/media/as-tabular-lesson2-tiw-name.png)
  
6.  在 [模擬資訊] 頁面中，您必須指定 Analysis Services 在匯入和處理資料時，用來連接資料來源的認證。 確認已選取 [特定的 Windows 使用者名稱和密碼]，然後在 [使用者名稱] 和 [密碼] 中輸入您的 Windows 登入認證，再按一下 [下一步]。  
  
    > [!NOTE]  
    > 使用 Windows 使用者帳戶和密碼可提供連接資料來源的最安全方法。 如需詳細資訊，請參閱[模擬](../analysis-services/tabular-models/impersonation-ssas-tabular.md)。  
  
7.  在 [選擇如何匯入資料] 頁面中，確認已選取 [從資料表和檢視表清單來選取要匯入的資料]。 若要從資料表和檢視表的清單中選取，請按一下 [下一步] 顯示來源資料庫內所有來源資料表的清單。  
  
8.  在 [選取資料表和檢視表] 頁面中，選取下列資料表的核取方塊：**DimCustomer**、**DimDate**、**DimGeography**、**DimProduct**、**DimProductCategory**、**DimProductSubcategory** 和 **FactInternetSales**。  
  
    **請不要**按一下 [完成]。  
  
## <a name="FilterData"></a>Filter the table data  
從範例資料庫匯入的 DimCustomer 資料表包含原始 SQL Server Adventure Works 資料庫中資料的子集。 您會篩選掉一些不需要匯入到您的模型時從 DimCustomer 資料表資料行。 如果可能的話，您要篩選掉不會使用以節省記憶體中模型所使用的空間資料。  
  
#### <a name="to-filter-the-table-data-prior-to-importing"></a>若要在匯入之前篩選資料表資料  
  
1.  選取的資料列**DimCustomer**資料表，然後按一下 **預覽和篩選**。 [預覽選取的資料表] 視窗隨即開啟，其中會顯示 DimCustomer 來源資料表內的所有資料行。  
  
2.  在下列資料行最上方的核取方塊： **SpanishEducation**， **FrenchEducation**， **SpanishOccupation**， **FrenchOccupation**. 

    ![做為表格式-第 2 課-tiw-清除](../analysis-services/media/as-tabular-lesson2-tiw-clear.png)
  
    因為這些資料行的值與網際網路銷售分析無關，所以不需要匯入這些資料行。 消除不必要的資料行可讓您的模型更小且更有效率。  
  
3.  確認已檢查過所有其他資料行，然後按一下 [確定]。  
  
    請注意單字**套用的篩選**現在會顯示在**篩選詳細資料**中的資料行**DimCustomer**資料列; 如果您按一下該連結，您會看到的文字描述您剛才套用的篩選條件。  
    
    ![做為表格式-第 2 課-套用的篩選](../analysis-services/media/as-tabular-lesson2-applied-filters.png)
    
  
4.  藉由清除每個資料表中下列資料行的核取方塊，篩選其餘資料表：  
    
    **DimDate**
    
      |資料行|  
      |--------|  
      |**DateKey**|  
      |**SpanishDayNameOfWeek**|  
      |**FrenchDayNameOfWeek**|  
      |**SpanishMonthName**|  
      |**FrenchMonthName**|  
  
    **DimGeography**
  
      |資料行|  
      |-------------|  
      |**SpanishCountryRegionName**|  
      |**FrenchCountryRegionName**|  
      |**IpAddressLocator**|  
  
    **DimProduct**
  
      |資料行|  
      |-----------|  
      |**SpanishProductName**|  
      |**FrenchProductName**|  
      |**FrenchDescription**|  
      |**ChineseDescription**|  
      |**ArabicDescription**|  
      |**HebrewDescription**|  
      |**ThaiDescription**|  
      |**GermanDescription**|  
      |**JapaneseDescription**|  
      |**TurkishDescription**|  
  
    **DimProductCategory**
  
      |資料行|  
      |--------------------|  
      |**SpanishProductCategoryName**|  
      |**FrenchProductCategoryName**|  
  
    **DimProductSubcategory**
  
      |資料行|  
      |-----------------------|  
      |**SpanishProductSubcategoryName**|  
      |**FrenchProductSubcategoryName**|  
  
    **FactInternetSales**
  
      |資料行|  
      |------------------|  
      |**OrderDateKey**|  
      |**DueDateKey**|  
      |**ShipDateKey**|   
  
## <a name="Import"></a>Import the selected tables and column data  
現在，您已預覽並篩選掉不必要的資料，您可以匯入其他您想資料。 此精靈會匯入資料表資料，包含資料表之間的任何關聯性。 在模型中建立新的資料表和資料行並不會匯入您篩選掉的資料。  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a>若要匯入選取的資料表和資料行資料  
  
1.  檢閱您的選取項目。 如果無誤，請按一下**完成**。  
  
    當匯入資料時，精靈會顯示已經提取的資料列數。 所有資料都匯入之後，就會顯示一則訊息，指出此作業已順利完成。  
    
    ![做為表格式-第 2 課-成功](../analysis-services/media/as-tabular-lesson2-success.png) 
  
    > [!TIP]  
    > 若要查看在匯入的資料表之間自動建立的關聯性，請在 [資料準備] 資料列上按一下 [詳細資料]。 
  
2.  按一下 [ **關閉**]。  
  
    關閉精靈並在模型設計師現在會顯示您匯入的資料表。 
  
## <a name="save-your-model-project"></a>儲存模型專案  
請務必經常儲存模型專案。  
  
#### <a name="to-save-the-model-project"></a>若要儲存模型專案  
  
-   按一下**檔案** > **儲存所有**。  
  
## <a name="whats-next"></a>下一步
移至下一課：[第 3 課： 標記為日期資料表](../analysis-services/lesson-3-mark-as-date-table.md)。

  
  
