---
title: Analysis Services 教學課程第 2 課： 取得資料 |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9adeebfbd3c49761adb816a7d28472a61ffca5cc
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38007199"
---
# <a name="get-data"></a>取得資料

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在這一課，您可以使用**取得資料**若要連接到 AdventureWorksDW 範例資料庫，選取資料、 預覽和篩選條件，，然後匯入到您的模型工作區。  
  
藉由使用 取得資料，您可以從各種來源匯入資料。 資料也可查詢使用 Power Query M 公式運算式或[原生 SQL 查詢運算式](../tabular-models/ssas-import-query.md)。

> [!NOTE]
> 工作和映像，在本教學課程會示範連接到內部部署伺服器上的 AdventureWorksDW2014 資料庫。 在某些情況下，Azure SQL 資料倉儲上的 AdventureWorksDW 資料庫可能會顯示不同的物件;不過，它們基本上都相同。
  
完成本課程的估計時間： **10 分鐘**  
  
## <a name="prerequisites"></a>先決條件  

這篇文章是表格式模型化教學課程中，應該依序完成的一部分。 執行工作之前在這一課，您應已完成上一課：[第 1 課： 建立新的表格式模型專案](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md)。  
  
## <a name="create-a-connection"></a>建立連接  
  
#### <a name="to-create-a-connection-to-the-adventureworksdw-database"></a>若要建立 AdventureWorksDW 資料庫的連接  
  
1.  在 **表格式模型總管**，以滑鼠右鍵按一下**資料來源** > **從資料來源匯入**。  
  
    這會啟動**取得資料**，其會引導您透過連接到資料來源。 如果您沒有看到 [表格式模型總管] 中，在**方案總管**，按兩下**Model.bim**設計工具中開啟模型。 
    
    ![as-lesson2-getdata](../tutorial-tabular-1400/media/as-lesson2-getdata.png)
  
2.  在 [取得資料]，按一下**資料庫** > **SQL Server 資料庫** > **Connect**。  
  
3.  在  **SQL Server 資料庫**對話方塊，請在**伺服器**，輸入您安裝 AdventureWorksDW 資料庫的伺服器名稱，然後按一下**Connect**。  

4.  當系統提示您輸入認證時，您必須指定 Analysis Services 用來連接到資料來源匯入和處理資料時的認證。 在 **模擬模式**，選取**模擬帳戶**，然後輸入認證，然後按一下  **Connect**。 建議您使用的帳戶密碼未過期。

    ![as-lesson2-account](../tutorial-tabular-1400/media/as-lesson2-account.png)
  
    > [!NOTE]  
    > 使用 Windows 使用者帳戶和密碼可提供連接資料來源的最安全方法。
  
5.  在 導覽器中，選取**AdventureWorksDW**資料庫，然後再按一下**確定**。這會建立資料庫的連接。 
  
6.  在 導覽器中，選取下列資料表的核取方塊： **DimCustomer**， **DimDate**， **DimGeography**， **DimProduct**， **DimProductCategory**， **DimProductSubcategory**，以及**FactInternetSales**。  

    ![為-lesson2-選取-資料表](../tutorial-tabular-1400/media/as-lesson2-select-tables.png)
  
按一下 確定 後，會開啟 查詢編輯器。 在下一步 區段中，您可以選取只想要匯入的資料。

  
## <a name="filter-the-table-data"></a>篩選資料表資料  

AdventureWorksDW 範例資料庫中的資料表有不需要在模型中包含的資料。 如果可能的話，您會想要篩選掉不必要的資料，以節省模型所使用的記憶體空間。 您篩選掉某些從資料表資料行，這樣就無法匯入工作空間資料庫或模型資料庫部署完成後。 
  
#### <a name="to-filter-the-table-data-before-importing"></a>若要匯入之前篩選資料表資料  
  
1.  在 [查詢編輯器] 中，選取**DimCustomer**資料表。 此時會出現 資料來源 （AdventureWorksDW 範例資料庫） 上的 DimCustomer 資料表檢視。 
  
2.  複選 （Ctrl + 按一下） **SpanishEducation**， **FrenchEducation**， **SpanishOccupation**， **FrenchOccupation**，然後以滑鼠右鍵按一下，然後**移除資料行**。 

    ![as-lesson2-remove-columns](../tutorial-tabular-1400/media/as-lesson2-remove-columns.png)
  
    因為這些資料行的值與網際網路銷售分析無關，所以不需要匯入這些資料行。 消除不必要的資料行可讓您的模型，更小且更有效率。  

    > [!TIP]
    > 如果您犯了，您可以藉由刪除中的步驟來備份**套用的步驟**。   
    
    ![as-lesson2-remove-columns](../tutorial-tabular-1400/media/as-lesson2-remove-step.png)

  
4.  每個資料表中移除下列資料行，以篩選其餘資料表：  
    
    **DimDate**
    
      |「資料行」|  
      |--------|  
      |**DateKey**|  
      |**SpanishDayNameOfWeek**|  
      |**FrenchDayNameOfWeek**|  
      |**SpanishMonthName**|  
      |**FrenchMonthName**|  
  
    **DimGeography**
  
      |「資料行」|  
      |-------------|  
      |**SpanishCountryRegionName**|  
      |**FrenchCountryRegionName**|  
      |**IpAddressLocator**|  
  
    **DimProduct**
  
      |「資料行」|  
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
  
      |「資料行」|  
      |--------------------|  
      |**SpanishProductCategoryName**|  
      |**FrenchProductCategoryName**|  
  
    **DimProductSubcategory**
  
      |「資料行」|  
      |-----------------------|  
      |**SpanishProductSubcategoryName**|  
      |**FrenchProductSubcategoryName**|  
  
    **FactInternetSales**
  
      沒有資料行中移除。
  
## <a name="Import"></a>Import the selected tables and column data  

既然您已預覽並篩選掉不必要的資料，您可以匯入您想的資料的其餘部分。 此精靈會匯入資料表資料，包含資料表之間的任何關聯性。 模型中建立新的資料表和資料行，並不會匯入您篩選掉的資料。  
  
#### <a name="to-import-the-selected-tables-and-column-data"></a>若要匯入選取的資料表和資料行資料  
  
1.  檢閱您的選取項目。 如果確認無誤，請按一下**匯入**。 資料處理 對話方塊會顯示正在從您的資料來源匯入至您的工作區資料庫的資料狀態。
  
    ![做為第 2 課成功](../tutorial-tabular-1400/media/as-lesson2-success.png) 
  
2.  按一下 [ **關閉**]。  

  
## <a name="save-your-model-project"></a>儲存模型專案  

請務必經常儲存模型專案。  
  
#### <a name="to-save-the-model-project"></a>若要儲存模型專案  
  
-   按一下 **檔案** > **全部儲存**。  
  
## <a name="whats-next"></a>下一步

[第 3 課： 標記為日期資料表](../tutorial-tabular-1400/as-lesson-3-mark-as-date-table.md)。

  
  
