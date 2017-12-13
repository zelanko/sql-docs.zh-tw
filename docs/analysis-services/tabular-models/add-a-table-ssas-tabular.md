---
title: "加入資料表 (SSAS 表格式) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d713c432-db99-4983-acc1-52b0fdd58bd6
caps.latest.revision: "5"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: b1ac605d76c4fe96354dc3365e7b9cccd2950988
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="add-a-table-ssas-tabular"></a>加入資料表 (SSAS 表格式)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]本主題描述如何將資料表加入資料來源的從中先前匯入資料模型。 若要從相同的資料來源加入資料表，您可以使用現有的資料來源連接。 從單一資料來源匯入任何數目的資料表時，建議您一律使用單一連接。  
  
### <a name="to-add-a-table-from-an-existing-data-source"></a>若要從現有的資料來源加入資料表  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，按一下 **[模型]** 功能表，然後再按一下 **[現有連接]**。  
  
2.  在 [現有連接] 頁面上，選取具有您想要加入之資料表的資料來源連接，然後按一下 [開啟]。  
  
3.  在 [選取資料表和檢視表] 頁面上，選取您想要從資料來源加入至模型的資料表。  
  
    > [!NOTE]  
    >  [選取資料表和檢視表] 頁面不會將顯示先前匯入的資料表顯示成已核取。  如果您選取了先前使用此連接來匯入的資料表，而且沒有為資料表提供不同的易記名稱，系統就會將 1 附加至易記名稱。 您不需要重新選取先前使用此連接來匯入的任何資料表。  
  
4.  必要時，請使用 [預覽和篩選] 來單獨選取特定資料行或將篩選套用至要匯入的資料。  
  
5.  按一下 [完成] 已匯入新的資料表。  
  
> [!NOTE]  
>  同時從單一資料來源匯入多個資料表時，系統將自動在模型中建立這些位於來源之資料表之間的任何關聯性。 不過，之後加入資料表時，您可能必須在模型中手動建立新加入資料表與先前匯入資料表之間的關聯性。  
  
## <a name="see-also"></a>請參閱  
 [匯入資料 (SSAS 表格式)](http://msdn.microsoft.com/library/6617b2a2-9f69-433e-89e0-4c5dc92982cf)   
 [刪除資料表 &#40;SSAS 表格式&#41;](../../analysis-services/tabular-models/delete-a-table-ssas-tabular.md)  
  
  
