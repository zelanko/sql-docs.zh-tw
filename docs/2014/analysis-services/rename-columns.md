---
title: 第 3 課： 重新命名資料行 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5fc8ba1a-2b30-4775-9b3b-c09dee711b3e
caps.latest.revision: 19
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6d4f9d156889bd3a761cff2a18a908df42e8aade
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37246096"
---
# <a name="lesson-3-rename-columns"></a>第 3 課：重新命名資料行
  在這一課，您將重新命名匯入的每個資料表中的多個資料行。 重新命名可讓資料行更容易識別，且更容易在模型設計師中以及藉由使用者在用戶端應用程式中選取欄位的方式進行導覽。 若要深入了解，請參閱[重新命名資料表或資料行 &#40;SSAS 表格式&#41;](tabular-models/rename-a-table-or-column-ssas-tabular.md)。  
  
> [!IMPORTANT]  
>  重新命名資料行不是完成本教學課程的必要工作；不過，在其餘課程 (尤其是包含建立關聯性的課程，以及使用 DAX 公式建立導出資料行和量值的課程) 會參考本課程中所述的資料行易記名稱。 如果您選擇不重新命名資料行，則必須在第 5、6 和 7 課中編輯 DAX 公式，以便使用本課中提供的原始來源資料行名稱。  
  
 完成本課程的估計時間： **20 分鐘**  
  
## <a name="prerequisites"></a>先決條件  
 本主題是表格式模型教學課程的一部分，必須依序完成。 在執行本課中的工作之前，您應已完成上一課： [第 2 課：新增資料](lesson-2-add-data.md)。  
  
## <a name="rename-columns"></a>重新命名資料行  
  
#### <a name="to-rename-columns"></a>若要重新命名資料行  
  
1.  在模型設計師中，按一下 [Customer] 資料表 (索引標籤)。  
  
     當您按一下某個索引標籤時，該資料表會在模型設計師視窗中變成使用中。  
  
2.  按兩下**CustomerKey**資料行名稱，然後輸入`Customer  Id`，然後按 ENTER 鍵。  
  
    > [!TIP]  
    >  您也可以在資料行之 [屬性] 視窗的 [資料行名稱] 屬性中，或是 [圖表檢視] 中，重新命名資料行。  
  
3.  重新命名 [Customer] 資料表中的其餘資料行以及其餘資料表中的資料行，使用易記名稱取帶來原名稱：  
  
     **Customer 資料表**  
  
    |來源名稱|易記名稱|  
    |-----------------|-------------------|  
    |GeographyKey|Geography Id|  
    |CustomerAlternateKey|Customer Alternate Id|  
    |FirstName|First Name|  
    |MiddleName|Middle Name|  
    |LastName|Last Name|  
    |NameStyle|Name Style|  
    |BirthDate|Birth Date|  
    |MaritalStatus|Marital Status|  
    |EmailAddress|Email Address|  
    |YearlyIncome|Yearly Income|  
    |TotalChildren|Total Children|  
    |NumberChildrenAtHome|Number of Children At Home|  
    |EnglishEducation|Education|  
    |EnglishOccupation|Occupation|  
    |HouseOwnerFlag|Owns House|  
    |NumberCarsOwned|Number of Cars Owned|  
    |AddressLine1|Address Line 1|  
    |AddressLine2|Address Line 2|  
    |Phone|Phone Number|  
    |DateFirstPurchase|Date of First Purchase|  
    |CommuteDistance|Commute Distance|  
  
     **Date**  
  
    |來源名稱|易記名稱|  
    |-----------------|-------------------|  
    |FullDateAlternateKey|date|  
    |DayNumberOfWeek|Day Number of Week|  
    |EnglishDayNameOfWeek|Day Name|  
    |DayNumberOfMonth|Day of Month|  
    |DayNumberOfYear|Day of Year|  
    |WeekNumberOfYear|Week Number of Year|  
    |EnglishMonthName|Month Name|  
    |MonthNumberOfYear|Month|  
    |CalendarQuarter|Calendar Quarter|  
    |CalendarYear|Calendar Year|  
    |CalendarSemester|Calendar Semester|  
    |FiscalQuarter|Fiscal Quarter|  
    |FiscalYear|Fiscal Year|  
    |FiscalSemester|Fiscal Semester|  
  
     **地理位置**  
  
    |來源名稱|易記名稱|  
    |-----------------|-------------------|  
    |GeographyKey|Geography Id|  
    |StateProvinceCode|State Province Code|  
    |StateProvinceName|State Province Name|  
    |CountryRegionCode|Country Region Code|  
    |EnglishCountryRegionName|Country Region Name|  
    |PostalCode|Postal Code|  
    |SalesTerritoryKey|Sales Territory Id|  
  
     **產品**  
  
    |來源名稱|易記名稱|  
    |-----------------|-------------------|  
    |ProductKey|Product Id|  
    |ProductAlternateKey|Product Alternate Id|  
    |ProductSubcategoryKey|Product Subcategory Id|  
    |WeightUnitMeasureCode|Weight Unit Code|  
    |SizeUnitMeasureCode|Size Unit Code|  
    |EnglishProductName|產品名稱|  
    |StandardCost|Standard Cost|  
    |FinishedGoodsFlag|Is Finished Product|  
    |SafetyStockLevel|Safety Stock Level|  
    |ReorderPoint|Reorder Point|  
    |ListPrice|List Price|  
    |SizeRange|Size Range|  
    |DaysToManufacture|Days to Manufacture|  
    |ProductLine|Product Line|  
    |Dealer Price|Dealer Price|  
    |ModelName|Model Name|  
    |LargePhoto|Large Photo|  
    |EnglishDescription|描述|  
    |StartDate|Product Start Date|  
    |EndDate|Product End Date|  
    |[狀態]|Product Status|  
  
     **產品類別目錄**  
  
    |來源名稱|易記名稱|  
    |-----------------|-------------------|  
    |ProductCategoryKey|Product Category Id|  
    |ProductCategoryAlternateKey|Product Category Alternate Id|  
    |EnglishProductCategoryName|Product Category Name|  
  
     **產品子類別目錄**  
  
    |來源名稱|易記名稱|  
    |-----------------|-------------------|  
    |ProductSubcategoryKey|Product Subcategory Id|  
    |ProductSubcategoryAlternateKey|Product Subcategory Alternate Id|  
    |EnglishProductSubcategoryName|Product Subcategory Name|  
    |ProductCategoryKey|Product Category Id|  
  
     **Internet Sales**  
  
    |來源名稱|易記名稱|  
    |-----------------|-------------------|  
    |ProductKey|Product Id|  
    |CustomerKey|Customer Id|  
    |PromotionKey|Promotion Id|  
    |CurrencyKey|Currency Id|  
    |SalesTerritoryKey|Sales Territory Id|  
    |SalesOrderNumber|Sales Order Number|  
    |SalesOrderLineNumber|Sales Order Line Number|  
    |RevisionNumber|修訂號碼|  
    |OrderQuantity|Order Quantity|  
    |UnitPrice|單價|  
    |ExtendedAmount|擴充量|  
    |UnitPriceDiscountPct|Unit Price Discount Pct|  
    |DiscountAmount|折扣量|  
    |ProductStandardCost|產品標準成本|  
    |TotalProductCost|產品總成本|  
    |SalesAmount|銷售量|  
    |TaxAmt|稅額|  
    |CarrierTrackingNumber|Carrier Tracking Number|  
    |CustomerPONumber|Customer PO Number|  
    |OrderDate|Order Date|  
    |DueDate|Due Date|  
    |ShipDate|Ship Date|  
  
## <a name="next-step"></a>下一個步驟  
 若要繼續進行本教學課程，請前往下一課： [第 4 課：標記為日期資料表](lesson-3-mark-as-date-table.md)。  
  
  
