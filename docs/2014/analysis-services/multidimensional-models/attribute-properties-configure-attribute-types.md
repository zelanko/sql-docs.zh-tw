---
title: 設定屬性類型 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- time dimensions [Analysis Services]
- attributes [Analysis Services], types
- slowly changing dimensions
- account dimensions [Analysis Services]
- currency dimensions [Analysis Services]
- Type property
ms.assetid: c2c6a3da-555e-4362-a83f-88da28427520
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e5223444f58326b7530388f3fe2fc06d72488a5e
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66077394"
---
# <a name="configure-attribute-types"></a>設定屬性類型
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中，屬性類型有助於從商務功能上將屬性分類。 屬性類型有很多，而且大部份可供用戶端應用程式用來顯示或支援屬性。 不過，有些屬性類型對 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]也有特定意義。 例如，有些屬性類型會針對時間維度，識別代表各種日曆之時間週期的屬性。  
  
##  <a name="setting_attibute_types"></a> 設定屬性類型  
 屬性 (Attribute) 之 `Type` 屬性 (Property) 的值決定該屬性 (Attribute) 的屬性 (Attribute) 類型。 定義維度或屬性時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的數個精靈會設定屬性類型。 這些 [ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 精靈] 將其他功能加入維度時，也會設定屬性類型。 例如，當商業智慧精靈加入帳戶智慧來識別包含維度之名稱、程式碼、號碼和帳戶結構的屬性時，精靈會將數個屬性類型套用至維度中的屬性。 商業智慧精靈也會耗用屬性類型，例如貨幣的轉換。 如需詳細資訊，請參閱 [建立貨幣類型維度](database-dimensions-create-a-currency-type-dimension.md)。  
  
 下表列出 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]可用的屬性類型。 這些資料表將屬性類型分成下列類別目錄：  
  
|詞彙|定義|  
|----------|----------------|  
|[一般屬性類型](#general_attribute_types)|這些值可供所有屬性使用，而且只用於讓用戶端應用程式進行屬性分類。|  
|[帳戶維度屬性類型](#account_dimension_attribute_types)|這些值會識別屬於帳戶維度的屬性。 如需帳戶維度的詳細資訊，請參閱 [建立父子式類型維度的財務帳戶](database-dimensions-finance-account-of-parent-child-type.md)。|  
|[貨幣維度屬性類型](#currency_dimension_attribute_types)|這些值會識別屬於貨幣維度的屬性。 如需貨幣維度的詳細資訊，請參閱 [建立貨幣類型維度](database-dimensions-create-a-currency-type-dimension.md)。|  
|[緩時變維度屬性](#slowly_changing_dimension_attribute_types)|這些值會識別屬於緩時變維度的屬性。|  
|[時間維度屬性](#time_dimension_attribute_types)|這些值會識別屬於時間維度的屬性。 如需時間維度的詳細資訊，請參閱 [建立日期類型維度](database-dimensions-create-a-date-type-dimension.md)。|  
  
###  <a name="general_attribute_types"></a> General Attribute Types  
  
|屬性類型值|描述|  
|--------------------------|-----------------|  
|`Address`|代表地址。|  
|`AddressBuilding`|代表地址的建築物識別碼。|  
|`AddressCity`|代表地址的城市。|  
|`AddressCountry`|代表地址的國家或地區。|  
|`AddressFax`|代表傳真電話號碼。|  
|`AddressFloor`|代表地址的樓層識別碼。|  
|`AddressHouse`|代表地址的房屋號碼。|  
|`AddressPhone`|代表電話號碼。|  
|`AddressQuarter`|代表地址的宅所。|  
|`AddressRoom`|代表地址的房間識別碼。|  
|`AddressStateOrProvince`|代表地址的州或省。|  
|`AddressStreet`|代表地址的街。|  
|`AddressZip`|代表地址的郵遞區號。|  
|`BomResource`|代表用料表 (BOM) 的資源。|  
|`Caption`|代表標題。|  
|`CaptionAbbreviation`|代表縮寫。|  
|`CaptionDescription`|代表描述。|  
|`Channel`|代表通路。|  
|`City`|代表縣 (市)。|  
|`Company`|代表公司。|  
|`Continent`|代表大陸。|  
|`Country`|代表國家或地區。|  
|`County`|代表國家 (地區)。|  
|`CustomerGroup`|代表客戶的群組。|  
|`CustomerHousehold`|代表客戶家庭成員。|  
|`Customers`|代表客戶。|  
|`DateCanceled`|代表取消日期。|  
|`DateDuration`|代表持續時間。|  
|`DateEnded`|代表結束日期。|  
|`DateModified`|代表修改日期。|  
|`DateStart`|代表開始日期。|  
|**DeletedFlag**|指出是否要刪除或應刪除成員 (在商務功能上)。<br /><br /> 注意： [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 不會使用此屬性類型來決定是否要刪除成員。 反之，此屬性類型只是為了供用戶端應用程式顯示而已。|  
|`FormattingColor`|代表格式化使用的色彩。|  
|`FormattingFont`|代表格式化使用的字型。|  
|`FormattingFontEffects`|代表格式化使用的字型效果。|  
|`FormattingFontSize`|代表格式化使用的字型大小。|  
|`FormattingOrder`|代表格式化使用的順序。|  
|`FormattingSubtotal`|代表小計。|  
|`GeoBoundaryBottom`|代表地理界限的最底部值。|  
|`GeoBoundaryFront`|代表地理界限的最前方值。|  
|`GeoBoundaryLeft`|代表地理界限的最左方值。|  
|`GeoBoundaryPolygon`|代表地理界限的多邊形定義。|  
|`GeoBoundaryRear`|代表地理界限的最後方值。|  
|`GeoBoundaryRight`|代表地理界限的最右方值。|  
|`GeoBoundaryTop`|代表地理界限的最頂部值。|  
|`GeoCentroidX`|代表地理區域的 X 軸距心。|  
|`GeoCentroidY`|代表地理區域的 Y 軸距心。|  
|`GeoCentroidZ`|代表地理區域的 Z 軸距心。|  
|`ID`|代表識別碼 (ID) 或索引鍵。|  
|`Image`|代表未定義之圖形格式的影像。|  
|`ImageBmp`|代表點陣圖圖形格式的影像。|  
|`ImageGif`|代表圖形交換格式 (GIF) 圖形格式的影像。|  
|`ImageJpg`|代表 JPEG 圖形格式的影像。|  
|`ImagePng`|代表可攜式網路圖形 (PNG) 圖形格式的影像。|  
|`ImageTiff`|代表 TIFF 圖形格式的影像。|  
|`OrganizationalUnit`|代表組織單位。|  
|`OrgTitle`|代表組織標題。|  
|`PercentOwnership`|代表擁有權百分比。|  
|`PercentVoteRight`|代表投票權的百分比。|  
|`Person`|代表個人。|  
|`PersonContact`|代表個人的連絡資訊。|  
|`PersonDemographic`|代表個人的人口統計資訊。|  
|`PersonFirstName`|代表個人的名字。|  
|`PersonFullName`|代表個人的全名。|  
|`PersonLastName`|代表個人的姓氏。|  
|`PersonMiddleName`|代表個人的中間名。|  
|`PhysicalColor`|代表色彩。|  
|`PhysicalDensity`|代表密度。|  
|`PhysicalDepth`|代表深度。|  
|`PhysicalHeight`|代表高度。|  
|`PhysicalSize`|代表大小。|  
|`PhysicalVolume`|代表體積。|  
|`PhysicalWeight`|代表重量。|  
|`PhysicalWidth`|代表寬度。|  
|`Point`|代表點。|  
|`PostalCode`|代表郵遞區號。|  
|`Product`|代表產品。|  
|`ProductBrand`|代表產品品牌。|  
|`ProductCategory`|代表產品類別目錄。|  
|`ProductGroup`|代表產品群組。|  
|`ProductSKU`|代表產品存貨保持單元 (SKU)。|  
|`Project`|代表專案。|  
|`ProjectCode`|代表專案代碼。|  
|`ProjectCompletion`|代表專案的完成狀態。|  
|`ProjectEndDate`|代表專案結束日期。|  
|`ProjectName`|代表專案名稱。|  
|`ProjectStartDate`|代表專案開始日期。|  
|`Promotion`|代表促銷。|  
|`QtyRangeHigh`|代表數量範圍的最大值。|  
|`QtyRangeLow`|代表數量範圍的最小值。|  
|`Quantitative`|代表數量的屬性。|  
|`Rate`|代表比率。|  
|`RateType`|代表比率類型。|  
|`Region`|代表客戶自訂的區域。|  
|`Regular`|代表一般屬性。|  
|`RelationToParent`|代表與父系的關聯性。|  
|`Representative`|表示代表。|  
|`Scenario`|代表狀況。|  
|`Sequence`|代表順序屬性。|  
|`ShortCaption`|代表簡短標題。|  
|`StateOrProvince`|代表省份。|  
|`Utility`|代表公用程式。|  
|`Version`|代表版本。|  
|`WebHtml`|代表 HTML 內容。|  
|`WebMailAlias`|代表電子郵件別名。|  
|`WebUrl`|代表 URL 位址。|  
|`WebXmlOrXsl`|代表 XML 或 XSL 內容。|  
  
###  <a name="account_dimension_attribute_types"></a> Account Dimension Attribute Types  
  
|屬性類型值|描述|  
|--------------------------|-----------------|  
|`Account`|代表帳戶的父系。 此屬性類型通常會套用至帳戶維度的父系屬性。|  
|`AccountName`|代表帳戶的名稱。 此屬性類型通常會套用至帳戶維度的索引鍵屬性。|  
|`AccountNumber`|代表帳戶的號碼。|  
|`AccountType`|代表帳戶的類型。 這個屬性類型會識別 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中帳戶類型維度內帳戶成員的彙總函式。|  
  
###  <a name="currency_dimension_attribute_types"></a> 貨幣維度屬性類型  
  
|屬性類型值|描述|  
|--------------------------|-----------------|  
|`CurrencyDestination`|代表貨幣兌換的目標貨幣。 此屬性類型通常會套用至報表維度的索引鍵屬性，以用於貨幣轉換。 如需貨幣轉換的詳細資訊，請參閱[貨幣轉換 &#40;Analysis Services&#41;](../currency-conversions-analysis-services.md)。|  
|`CurrencyIsoCode`|代表貨幣的國際標準組織 (ISO) 代碼。 如需貨幣轉換的詳細資訊，請參閱[貨幣轉換 &#40;Analysis Services&#41;](../currency-conversions-analysis-services.md)。|  
|`CurrencyName`|代表貨幣的名稱。 如需貨幣轉換的詳細資訊，請參閱[貨幣轉換 &#40;Analysis Services&#41;](../currency-conversions-analysis-services.md)。|  
|`CurrencySource`|代表貨幣兌換的來源貨幣。 此屬性類型通常會套用至貨幣維度的索引鍵屬性，以用於貨幣轉換。 如需貨幣轉換的詳細資訊，請參閱[貨幣轉換 &#40;Analysis Services&#41;](../currency-conversions-analysis-services.md)。|  
  
###  <a name="slowly_changing_dimension_attribute_types"></a> 緩時變維度屬性類型  
  
|屬性類型值|描述|  
|--------------------------|-----------------|  
|**ScdEndDate**|代表緩時變維度中的成員之有效結束日期。|  
|**ScdOriginalID**|代表緩時變維度中的成員之原始識別碼。|  
|**ScdStartDate**|代表緩時變維度中的成員之有效開始日期。|  
|`ScdStatus`|代表緩時變維度中的成員之有效狀態。|  
  
###  <a name="time_dimension_attribute_types"></a> 時間維度屬性類型  
  
|屬性類型值|描述|  
|--------------------------|-----------------|  
|`Date`|代表日期。 此屬性類型通常會套用至時間維度或伺服器時間維度的索引鍵屬性。|  
|`DayOfHalfYear`|代表半年中的日序數。|  
|`DayOfMonth`|代表月中的日序數。|  
|`DayOfQuarter`|代表季中的日序數。|  
|`DayOfTenDays`|代表十天週期中的日序數。|  
|`DayOfTrimester`|代表每四個月中的日序數。|  
|`DayOfWeek`|代表週中的日序數。|  
|`DayOfYear`|代表年中的日序數。|  
|`Days`|代表天數。|  
|`FiscalDate`|代表會計日曆中的日期。|  
|`FiscalDayOfHalfYear`|代表會計日曆中之半年的日序數。|  
|`FiscalDayOfMonth`|代表會計日曆中之月的日序數。|  
|`FiscalDayOfQuarter`|代表會計日曆中之季的日序數。|  
|`FiscalDayOfTrimester`|代表會計日曆中之每四個月的日序數。|  
|`FiscalDayOfWeek`|代表會計日曆中之週的日序數。|  
|`FiscalDayOfYear`|代表會計日曆中之年的日序數。|  
|`FiscalHalfYears`|代表會計日曆中的半年度。|  
|`FiscalHalfYearOfYear`|代表會計日曆中之年的半年度序數。|  
|`FiscalMonths`|代表會計日曆中的月份。|  
|`FiscalMonthOfHalfYear`|代表會計日曆中之半年度的月序數。|  
|`FiscalMonthOfQuarter`|代表會計日曆中之季的月序數。|  
|`FiscalMonthOfTrimester`|代表會計日曆中之每四個月的月序數。|  
|`FiscalMonthOfYear`|代表會計日曆中之年的月序數。|  
|`FiscalQuarters`|代表會計日曆中的季數。|  
|`FiscalQuarterOfHalfYear`|代表會計日曆中之半年的季序數。|  
|`FiscalQuarterOfYear`|代表會計日曆中之年的季序數。|  
|`FiscalTrimesters`|代表會計日曆中的每四個月。|  
|`FiscalTrimesterOfYear`|代表會計日曆中之年的每四個月序數。|  
|`FiscalWeeks`|代表會計日曆中的週。|  
|`FiscalWeekOfHalfYear`|代表會計日曆中之半年的週序數。|  
|`FiscalWeekOfMonth`|代表會計日曆中之月的週序數。|  
|`FiscalWeekOfQuarter`|代表會計日曆中之季的週序數。|  
|`FiscalWeekOfTrimester`|代表會計日曆中之每四個月的週序數。|  
|`FiscalWeekOfYear`|代表會計日曆中之年的週序數。|  
|`FiscalYears`|代表會計日曆中的年。|  
|`HalfYears`|代表半年度。|  
|`HalfYearOfYear`|代表年中的半年度序數。|  
|`Hours`|代表小時。|  
|`IsHoliday`|指出日期是否為假日。|  
|`ISO8601Date`|代表 ISO 8601 日曆中的日期。|  
|`ISO8601DayOfWeek`|代表 ISO 8601 日曆中之週的日序數。|  
|`ISO8601DayOfYear`|代表 ISO 8601 日曆中之年的日序數。|  
|`ISO8601Weeks`|代表 ISO 8601 日曆中的週。|  
|`ISO8601WeekOfYear`|代表 ISO 8601 日曆中之年的週序數。|  
|`ISO8601Years`|代表 ISO 8601 日曆中的年。|  
|`IsPeakDay`|指出日期是否為尖峰日。|  
|`IsWeekDay`|指出日期是否為工作日。|  
|`IsWorkingDay`|指出日期是否為工作日。|  
|`ManufacturingDate`|代表製造日曆中的日期。|  
|`ManufacturingDayOfHalfYear`|代表製造日曆中之半年的日序數。|  
|`ManufacturingDayOfMonth`|代表製造日曆中之月的日序數。|  
|`ManufacturingDayOfQuarter`|代表製造日曆中之季的日序數。|  
|`ManufacturingDayOfTrimester`|代表製造日曆中之每四個月的日序數。|  
|`ManufacturingDayOfWeek`|代表製造日曆中之週的日序數。|  
|`ManufacturingDayOfYear`|代表製造日曆中之年的日序數。|  
|`ManufacturingHalfYears`|代表製造日曆中的半年度。|  
|`ManufacturingHalfYearOfYear`|代表製造日曆中之年的半年度序數。|  
|`ManufacturingMonths`|代表製造日曆中的月份。|  
|`ManufacturingMonthOfHalfYear`|代表製造日曆中之半年的月序數。|  
|`ManufacturingMonthOfQuarter`|代表製造日曆中之季的月序數。|  
|`ManufacturingMonthOfTrimester`|代表製造日曆中之每四個月的月序數。|  
|`ManufacturingMonthOfYear`|代表製造日曆中之年的月序數。|  
|`ManufacturingQuarters`|代表製造日曆中的季數。|  
|`ManufacturingQuarterOfHalfYear`|代表製造日曆中之半年的季序數。|  
|`ManufacturingQuarterOfYear`|代表製造日曆中之年的季序數。|  
|`ManufacturingWeeks`|代表製造日曆中的週。|  
|`ManufacturingWeekOfHalfYear`|代表製造日曆中之半年的週序數。|  
|`ManufacturingWeekOfMonth`|代表製造日曆中之月的週序數。|  
|`ManufacturingWeekOfQuarter`|代表製造日曆中之季的週序數。|  
|`ManufacturingWeekOfTrimester`|代表製造日曆中之每四個月的週序數。|  
|`ManufacturingWeekOfYear`|代表製造日曆中之年的週序數。|  
|`ManufacturingYears`|代表製造日曆中的年。|  
|`Minutes`|代表分鐘數。|  
|`Months`|代表月份。|  
|`MonthOfHalfYear`|代表半年的月序數。|  
|`MonthOfQuarter`|代表季的月序數。|  
|`MonthOfTrimester`|代表每四個月的月序數。|  
|`MonthOfYear`|代表年中的月序數。|  
|`Quarters`|代表季數。|  
|`QuarterOfHalfYear`|代表半年中的季序數。|  
|`QuarterOfYear`|代表年中的季序數。|  
|`ReportingDate`|代表報表日曆中的日期。|  
|`ReportingDayOfHalfYear`|代表報表日曆中之半年的日序數。|  
|`ReportingDayOfMonth`|代表報表日曆中之月的日序數。|  
|`ReportingDayOfQuarter`|代表報表日曆中之季的日序數。|  
|`ReportingDayOfTrimester`|代表報表日曆中之每四個月的日序數。|  
|`ReportingDayOfWeek`|代表報表日曆中之週的日序數。|  
|`ReportingDayOfYear`|代表報表日曆中之年的日序數。|  
|`ReportingHalfYears`|代表報表日曆中的半年度。|  
|`ReportingHalfYearOfYear`|代表報表日曆中之年的半年度序數。|  
|`ReportingMonths`|代表報表日曆中的月份。|  
|`ReportingMonthOfHalfYear`|代表報表日曆中之半年的月序數。|  
|`ReportingMonthOfQuarter`|代表報表日曆中之季的月序數。|  
|`ReportingMonthOfTrimester`|代表報表日曆中之每四個月的月序數。|  
|`ReportingMonthOfYear`|代表報表日曆中之年的月序數。|  
|`ReportingQuarters`|代表報表日曆中的季數。|  
|`ReportingQuarterOfHalfYear`|代表報表日曆中之半年的季序數。|  
|`ReportingQuarterOfYear`|代表報表日曆中之年的季序數。|  
|`ReportingTrimesters`|代表報表日曆中的每四個月。|  
|`ReportingTrimesterOfYear`|代表報表日曆中之年的每四個月序數。|  
|`ReportingWeeks`|代表報表日曆中的週。|  
|`ReportingWeekOfHalfYear`|代表報表日曆中之半年的週序數。|  
|`ReportingWeekOfMonth`|代表報表日曆中之月的週序數。|  
|`ReportingWeekOfQuarter`|代表報表日曆中之季的週序數。|  
|`ReportingWeekOfTrimester`|代表報表日曆中之每四個月的週序數。|  
|`ReportingWeekOfYear`|代表報表日曆中之年的週序數。|  
|`ReportingYears`|代表報表日曆中的年。|  
|`Seconds`|代表秒數。|  
|`TenDayOfHalfYear`|代表半年的十天週期序數。|  
|`TenDayOfMonth`|代表月的十天週期序數。|  
|`TenDayOfQuarter`|代表季的十天週期序數。|  
|`TenDayOfTrimester`|代表每四個月的十天週期序數。|  
|`TenDayOfYear`|代表年的十天週期序數。|  
|`TenDays`|代表十天週期。|  
|`Trimesters`|代表每四個月。|  
|`TrimesterOfYear`|代表年的每四個月序數。|  
|`UndefinedTime`|代表未定義的時間週期。|  
|`WeekOfYear`|代表年的週序數。|  
|`Weeks`|代表週。|  
|**WinterSummerSeason**|指出日期是否為冬季/夏季的一部份。|  
|`Years`|代表年。|  
  
## <a name="see-also"></a>另請參閱  
 [屬性和屬性階層](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [維度屬性 (Attribute) 屬性 (Property) 參考](dimension-attribute-properties-reference.md)  
  
  
