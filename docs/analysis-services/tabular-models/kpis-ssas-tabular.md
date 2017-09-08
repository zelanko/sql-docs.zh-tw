---
title: "Kpi (SSAS 表格式) |Microsoft 文件"
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a0524602-5239-45a7-8c44-2477302a3637
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f4755d0271523b65073b72c6b06f6dec8cfcb90a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="kpis"></a>KPI
  表格式模型中的「關鍵效能指標」(KPI) 可用來針對由量值或絕對值定義的「目標」值，量測由「基底」量值定義之值的績效。 本主題為表格式模型作者提供對於表格式模型中 KPI 的基本了解。  
  
##  <a name="bkmk_benefits"></a> 優點  
 在商務用語中，關鍵效能指標 (KPI) 是量測商務目標的可量化度量。 KPI 通常會在一段時間內進行評估。 例如，組織的銷售部門可以使用 KPI，針對預計的毛利來測量每月的毛利。 會計部門可以針對營收測量每月支出，以評估成本，而人力資源部門可以測量每季員工營業額。 每一個都是 KPI 的範例。 商務專業人員經常會使用在商務計分卡中分組的 KPI，以取得商務成就之快速與精確的記錄摘要，或識別趨勢。  
  
 表格式模型中的 KPI 包括：  
  
 **基底值**  
 基底值是由解析為值的量值來定義。 例如，此值可以是實際銷售的彙總，也可以是指定期間內的導出量值，例如收益。  
  
 **目標值**  
 目標值是由解析為值的量值或由絕對值來定義。 例如，目標值可能是組織業務經理想要提升銷售或利潤所用的量。  
  
 **狀態臨界值**  
 狀態臨界值是由介於高低臨界值之間的範圍來定義，或由固定值來定義。 狀態臨界值會顯示圖形，幫助使用者輕鬆地判斷基底值相較於目標值的狀態。  
  
##  <a name="bkmk_example"></a> 範例  
 任職於 Adventure Works 的銷售經理想要建立樞紐分析表，用來快速顯示銷售員工是否達成給定期間 (年份) 的銷售配額。 對於每個銷售員工，她要樞紐分析表顯示實際銷售金額 (美元)、銷售配額量 (美元)，以及顯示每個銷售員工狀態是低於、等於或高於其銷售配額的簡單圖形。 她希望能依年份配量這些資料。  
  
 為了達成目的，銷售經理請組織的 BI 方案開發人員協助將銷售 KPI 加入至 AdventureWorks 表格式模型。 銷售經理將使用 Excel 來連接至 Adventure Works 表格式模型，做為資料來源，並具有欄位 （量值和 KPI） 和交叉分析篩選器來分析銷售主力達成其配額建立樞紐分析表。  
  
 在模型中，FactResellerSales 資料表的 SalesAmount 資料行上建立了量值，提供每個銷售員工的實際銷售金額 (美元)。 此量值會定義 KPI 的基底值。  
  
 Sales 量值是以下列公式建立的：  
  
```  
Sales:=Sum(FactResellerSales[SalesAmount])  
```  
  
 FactSalesQuota 資料表的 SalesAmountQuota 資料行為每個員工定義了銷售量配額。 此資料行的值會做為 KPI 的目標量值 (值)。  
  
 SalesAmountQuota 量值是以下列公式建立的：  
  
```  
Target SalesAmountQuota:=Sum(FactSalesQuota[SalesAmountQuota])  
```  
  
> [!NOTE]  
>  FactSalesQuota 資料表的 EmployeeKey 資料行和 DimEmployees 資料表的 EmployeeKey 之間有關聯性。 此關聯性為必要項，因此 DimEmployee 資料表中的每個銷售員工才能顯示在 FactSalesQuota 資料表中。  
  
 現在已建立量值做為 KPI 的基底值和目標值，Sales 量值就會延伸至新的銷售 KPI。 在銷售 KPI 中，目標 SalesAmountQuota 量值是定義為目標值。 狀態臨界值是定義為範圍百分比，其目標為 100%，表示 Sales 量值所定義的實際銷售符合目標 SalesAmoutnQuota 量值所定義的配額量。 高低百分比定義於狀態列，而且選取圖形類型。  
  
 銷售經理現在可以將 KPI 的基底值、目標值和狀態加入至 Values 欄位，藉以建立樞紐分析表。 Employees 資料行會加入至 RowLabel 欄位，而 CalendarYear 資料行則會加入為交叉分析篩選器。  
  
 銷售經理現在可以依年份來配量每個銷售員工的實際銷售金額、銷售配額量和狀態。 她可以分析數年來銷售趨勢，決定是否需要調整銷售員工的銷售配額。  
  
##  <a name="bkmk_create"></a> Create and edit KPIs  
 若要建立 KPI，請使用模型設計師中的 [關鍵效能指標] 對話方塊。 由於 KPI 必須與量值關聯，因此您可以透過擴充判斷為基底值的量值，然後建立判斷為目標值的量值或輸入絕對值，來建立 KPI。 定義基底量值 (基底值) 和目標值之後，即可定義基底值與目標值之間的狀態臨界值參數。 此狀態會以圖形格式顯示 (使用可選取的圖示、橫條、圖形或色彩)。 然後可將基底和目標值以及狀態，以可根據其他資料欄位分割的值形式加入報表或樞紐分析表。  
  
 若要檢視 [關鍵效能指標] 對話方塊，請在資料表的量值方格中，以滑鼠右鍵按一下做為基底值的量值，然後按一下 **[建立 KPI]**。 將量值擴充至 KPI 做為基底值之後，量值方格中的量值名稱旁會出現圖示，指出量值與 KPI 相關聯。  
  
##  <a name="bkmk_related_tasks"></a> 相關工作  
  
|主題|Description|  
|-----------|-----------------|  
|[建立及管理 Kpi](../../analysis-services/tabular-models/create-and-manage-kpis-ssas-tabular.md)|描述如何使用基底量值、目標量值及狀態臨界值建立 KPI。|  
  
## <a name="see-also"></a>另請參閱  
 [量值](../../analysis-services/tabular-models/measures-ssas-tabular.md)   
 [檢視方塊](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)  
  
  
