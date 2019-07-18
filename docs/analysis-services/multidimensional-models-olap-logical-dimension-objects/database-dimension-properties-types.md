---
title: 維度類型 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 663c26ac169c11e5ab2d9b90285419cf4145368c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63025773"
---
# <a name="database-dimension-properties---types"></a>資料庫維度屬性 - 類型
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  **型別**屬性設定會提供給伺服器和用戶端應用程式的維度內容的相關資訊。 在某些情況下，**型別**設定只會提供用戶端應用程式的指引，而且是選擇性。 在其他情況下，這類**帳戶**或是**時間**維度**型別**維度和其屬性的屬性設定會決定特定的伺服器型行為而且可能必須實作在 cube 中的特定行為。 例如，**型別**維度的屬性可以設為**帳戶**用戶端應用程式指出標準維度包含帳戶屬性。 如需時間、 帳戶和貨幣維度的詳細資訊，請參閱[建立日期類型維度](../../analysis-services/multidimensional-models/database-dimensions-create-a-date-type-dimension.md)，[建立的父子式類型維度的財務帳戶](../../analysis-services/multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md)，和[建立貨幣輸入維度](../../analysis-services/multidimensional-models/database-dimensions-create-a-currency-type-dimension.md)。  
  
 維度類型的預設設定**一般**，這可讓內容的維度做任何假設。 這是所有維度的預設設定，當您一開始定義維度，除非您指定**時間**定義維度使用 「 維度精靈 」 時。 您也應該保留**一般**做為維度類型，如果 「 維度精靈 」 不會列出維度類型的適當的型別。  
  
## <a name="available-dimension-types"></a>可用的維度類型  
 下表描述可用的維度類型[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。  
  
|維度類型|描述|  
|--------------------|-----------------|  
|一般|此維度的類型並未設定為特殊維度類型。|  
|Time|此維度的屬性代表時間週期，例如年數、半年數、季數、月數和日數。|  
|組織|此維度的屬性代表組織的資訊，例如員工或分公司。|  
|Geography|此維度的屬性代表地理資訊，例如城市或郵遞區號。|  
|BillOfMaterials|維度的屬性代表存貨或製造資訊 (例如產品的組件清單)。|  
|帳戶|此維度的屬性代表財務報表用途的帳戶圖表。|  
|客戶|此維度的屬性代表客戶或連絡資訊。|  
|產品|此維度的屬性代表產品資訊。|  
|狀況|此維度的屬性代表計畫或策略分析資訊。|  
|數量|此維度的屬性代表數量的資訊。|  
|公用程式|此維度的屬性代表其他資訊。|  
|Currency|此維度類型包含貨幣資料和中繼資料。|  
|匯率|此維度的屬性代表貨幣匯率的資訊。|  
|通路|此維度的屬性代表通道資訊。|  
|促銷|此維度的屬性代表行銷促銷資訊。|  
  
## <a name="see-also"></a>另請參閱  
 [使用現有的資料表建立維度](../../analysis-services/multidimensional-models/create-a-dimension-by-using-an-existing-table.md)   
 [維度 &#40;Analysis Services-多維度資料 &#41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  
