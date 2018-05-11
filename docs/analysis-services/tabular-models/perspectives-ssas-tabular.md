---
title: 檢視方塊 |Microsoft 文件
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9a9b8fd2c491b0220cc57c6e9558a849813136fa
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="perspectives"></a>檢視方塊
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  表格式模型中的檢視方塊會定義可檢視之模型子集，以提供具體的特定商務或應用程式模型視點。  
  
##  <a name="bkmk_understanding"></a> 優點  
 對於要瀏覽的使用者而言，表格式模型可以是很複雜的。 單一模型可能代表完整的資料倉儲內容，其中有許多資料表、量值和維度。 對只需要與模型的一小部分進行互動即可滿足其商業智慧和報表需求的使用者而言，這樣的複雜性令人望而生畏。  
  
 在檢視方塊中，資料表、資料行和量值 (包括 KPI) 是定義為欄位物件。 您可以為每個檢視方塊選取可檢視的欄位。 例如，單一模型可以包含產品、銷售、財務、員工和地理資料。 雖然銷售部門需要產品、銷售、促銷和地理資料，但可能不需要員工和財務資料。 同樣地，人力資源部門不需要促銷和地理資料。  
  
 當使用者連接到具有已定義檢視方塊的模型 (做為資料來源) 時，可以選取要使用的檢視方塊。 例如，當連接到 Excel 的模型資料來源時，人力資源使用者可以在 [資料連接精靈] 的 [選取資料表和檢視表] 頁面上選取 [人力資源] 檢視方塊。 只有為 [人力資源] 檢視方塊定義的欄位 (資料表、資料行及量值) 才會顯示在 [樞紐分析表欄位清單] 中。  
  
 檢視方塊並非用來做為安全性機制，而是用來提供較佳使用者體驗的工具。 特定檢視方塊的所有安全性，都是繼承自基礎模型。 如果使用者沒有模型物件的存取權，檢視方塊也無法提供這些存取權。 必須先解決模型資料庫的安全性，才能透過檢視方塊提供模型中物件的存取權。 您可使用安全性角色來保護模型中繼資料和資料的安全。 如需詳細資訊，請參閱[角色](../../analysis-services/tabular-models/roles-ssas-tabular.md)。  
  
##  <a name="bkmk_testpersp"></a> Testing perspectives  
 在撰寫模型時，您可以使用模型設計師中的 [在 Excel 中進行分析] 功能，來測試所定義之檢視方塊的效率。 請從模型設計師中的 **[模型]** 功能表，按一下 **[在 Excel 中進行分析]**， **[選擇認證和檢視方塊]** 對話方塊即會在 Excel 開啟前出現。 在這個對話方塊中，您可指定目前的使用者名稱、其他使用者、角色，以及您想用來連接至做為資料來源之模型工作空間資料庫並檢視資料的檢視方塊。  
  
##  <a name="bkmk_related_tasks"></a> Related tasks  
  
|主題|Description|  
|-----------|-----------------|  
|[建立及管理檢視方塊](../../analysis-services/tabular-models/create-and-manage-perspectives-ssas-tabular.md)|描述如何使用模型設計師中的 [檢視方塊] 對話方塊，以建立及管理檢視方塊。|  
  
## <a name="see-also"></a>另請參閱  
 [角色](../../analysis-services/tabular-models/roles-ssas-tabular.md)   
 [階層架構](../../analysis-services/tabular-models/hierarchies-ssas-tabular.md)  
  
  
