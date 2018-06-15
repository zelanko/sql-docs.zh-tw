---
title: DataSources 和 DataSets 集合參考 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f951a4aa-da55-4e43-8579-4a5d4480d11f
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b6e03491b893ac6c77a202207ff7e296ac20f153
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33022265"
---
# <a name="built-in-collections---datasources-and-datasets-references-report-builder"></a>內建集合 - DataSources 和 DataSets 參考 (報表產生器)
  **DataSources** 集合代表報表中使用的所有資料來源。 同樣地， **DataSets** 集合則代表報表中所有資料來源的所有資料集。 請使用 [報表資料] 窗格以階層的方式檢視報表資料集 (排列在所參考資料來源的下方)。 如果加入這些集合的參考，就不會在預覽報表時看到值。 只有發行報表至報表伺服器後，才可以使用這些集合。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="datasources"></a>DataSources  
 **DataSources** 集合代表已發行報表定義中參考的資料來源。 您可以選擇在報表中加入這項資訊，以記錄報表資料的來源。 這個集合在 [預覽] 模式中無法使用。 下表描述 **DataSources** 集合內的變數。  
  
|**變數**|**型別**|**說明**|  
|------------------|--------------|---------------------|  
|**DataSourceReference**|**String**|報表伺服器上資料來源定義的完整路徑。 例如，您可以包含報表用來做為報表記錄一部分的所有資料來源的清單。 以下範例將示範名為 AdventureWorks2012 的資料來源完整路徑：<br /><br /> `/DataSources/AdventureWorks2012`。|  
|**型別**|**String**|資料來源的資料提供者類型。 例如， `SQL`。|  
  
## <a name="datasets"></a>DataSets  
 **DataSets** 集合代表報表定義中參考的資料集。 您可以選擇將查詢加入報表的文字方塊中，這樣如果使用者想要知道報表中到底有什麼資料，就可以看到原始的命令文字。 這個集合在 [預覽] 模式中無法使用。 下表描述 **DataSets** 集合的成員。  
  
|**成員**|**型別**|**說明**|  
|----------------|--------------|---------------------|  
|**CommandText**|**String**|針對資料庫資料來源，此查詢是用來擷取資料來源中的資料。 如果查詢是運算式，則此為評估運算式。|  
|**RewrittenCommandText**|**String**|資料提供者的擴充 CommandText 值。 此值通常用於含有對應至報表參數之查詢參數的報表。 當命令文字參數參考擴充至針對已對應報表參數所選取的常數值時，資料提供者會設定此屬性。|  
  
### <a name="using-query-expressions"></a>使用查詢運算式  
 您可以利用運算式來定義資料集內包含的查詢。 您可以使用此功能來設計報表，在此報表中會根據使用者的輸入、其他資料集內的資料，或其他變數來變更查詢。 如需查詢的詳細資訊，請參閱[報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
 [運算式 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
