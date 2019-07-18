---
title: 產生時間資料表來建立時間維度 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- time dimensions [Analysis Services]
- dimensions [Analysis Services], time
- time periods [Analysis Services]
- range-based time dimensions [Analysis Services]
- server time dimensions [Analysis Services]
- calendars [Analysis Services]
- table-based time dimensions [Analysis Services]
ms.assetid: 58303326-1361-4c0e-9f3d-642ce69c4f6a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b54bfbdb03f6f2220cf66cb988456b2e6e6a0070
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66076285"
---
# <a name="create-a-time-dimension-by-generating-a-time-table"></a>Create a Time Dimension by Generating a Time Table
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，當來源資料庫中沒有任何可用的時間資料表時，您就可以使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的「維度精靈」來建立時間維度。 您可以透過在 **[選取建立方法]** 頁面上選取下列其中一個選項，完成此作業：  
  
-   **在資料來源中產生時間資料表** ：當您擁有在基礎資料來源中建立物件的權限時，請選取這個選項。 然後，這個精靈將產生時間資料表並將此資料表儲存在資料來源中。 接著，這個精靈會根據此時間資料表建立時間維度。  
  
-   **在伺服器上產生時間資料表** ：當您沒有在基礎資料來源中建立物件的權限時，請選取這個選項。 然後，這個精靈將在伺服器上 (而非資料來源中) 產生並儲存資料表 (根據伺服器之時間資料表所建立的維度稱為「伺服器時間維度」  )。接著，這個精靈會根據此資料表建立伺服器時間維度。  
  
 當您建立時間維度時，可以指定時間週期以及此維度的開始和結束日期。 精靈會使用指定的時間週期，來建立時間屬性。 當您處理維度時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 會產生和儲存支援指定之日期與週期所需的資料。 此精靈會使用針對時間維度所建立的屬性來建議此維度的階層。 階層會反映不同時間週期之間的關聯性，並且會考慮不同的日曆。 例如，在標準日曆階層中，週層級會在年層級之下顯示，而非在月層級之下顯示，因為週數可以完整地分配到年當中，但無法完整地分配到月當中。 相對地，在製造日曆或報表日曆階層中，週數可以完整地分配到月當中，因此週層級會在月層級之下顯示。  
  
## <a name="define-time-periods"></a>定義時間週期  
 您可以使用精靈的 **[定義時間週期]** 頁面，指定您要包含在維度中的日期範圍。 例如，您可以選取資料當中，從最早年度 1 月 1 日開始，並在目前年度的一或二年後結束的範圍 (以允許未來的交易)。 在此範圍之外的交易不會出現，或以維度的未知成員出現，視維度的 `UnknownMemberVisible` 屬性設定而定。 您也可以變更資料所使用的每週第一天 (預設為星期日)。  
  
 選取當精靈建立套用至資料的階層時要使用的時間週期，例如年、半年、季、每四個月、月、十天、週或日期。 您至少一定要選取日期時間週期。 Date 屬性是維度的索引鍵屬性，因此維度沒有它就無法作用。  
  
 在 **[時間成員名稱的語言]** 旁，選取要用來標示維度之成員的語言。  
  
 您建立以日期範圍為基礎的時間維度之後，可以使用維度設計師來加入或移除時間屬性。 由於 Date 屬性是維度的索引鍵屬性，因此不能從維度中移除該屬性。 若要對使用者隱藏 Date 屬性 (Attribute)，您可以將該屬性 (Attribute) 的 `AttributeHierarchyVisible` 屬性 (Property) 變更為 `False`。  
  
## <a name="select-calendars"></a>選取日曆  
 您建立時間維度時，一律會包含標準 (西曆) 12 個月日曆，從 1 月 1 日開始，到 12 月 31 日結束。 在精靈的 **[選取日曆]** 頁面上，可以指定此維度中之階層做為基礎的其他日曆。 如需日曆類型的描述，請參閱 [建立日期類型維度](database-dimensions-create-a-date-type-dimension.md)。  
  
 依據您在精靈 **[定義時間週期]** 頁面上選取的時間週期，日曆選取項目決定在維度中建立的屬性。 例如，您若在精靈的 [定義時間週期]  頁面上選取 [年]  和 [季]  時間週期，並在 [選取日曆]  頁面上選取 [會計日曆]  ，則會為會計日曆建立 FiscalYear、FiscalQuarter 和 FiscalQuarterOfYear 屬性。  
  
 精靈也會建立日曆特定階層，由針對日曆建立的屬性構成。 針對每一個日曆，每一個階層中的每個層級都會彙總至上一層級。 例如，標準的 12 個月日曆當中，精靈會建立年和週，或年和月的階層。 但是，在標準日曆中，每個月的週數並不平均，因此沒有年、月和週的階層。 相對地，報告或製造日曆中的週會平均分配到各月份，因此在這些日曆中，週會彙總至月。  
  
## <a name="completing-the-dimension-wizard"></a>完成維度精靈  
 在 **[正在完成精靈]** 頁面上，檢閱精靈所建立的屬性與階層，然後為時間維度命名。 按一下 **[完成]** 以完成精靈，並建立維度。 完成維度之後，您可以使用維度設計師來變更維度。  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型中的資料來源檢視](data-source-views-in-multidimensional-models.md)   
 [建立日期類型維度](database-dimensions-create-a-date-type-dimension.md)   
 [資料庫維度屬性](../multidimensional-models-olap-logical-dimension-objects/database-dimension-properties.md)   
 [維度關聯性](../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [使用現有的資料表建立維度](create-a-dimension-by-using-an-existing-table.md)   
 [在資料來源中產生非時間資料表來建立維度](create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md)  
  
  
