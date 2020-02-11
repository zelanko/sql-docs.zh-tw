---
title: 匯出（DMX） |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 622f575541d1a111e5cda6a28617ad400a977292
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68892801"
---
# <a name="export-dmx"></a>EXPORT (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  從伺服器中將採礦模型或採礦結構物件擷取到 Analysis Services 備份檔案 (.abf)。  
  
## <a name="syntax"></a>語法  
  
```  
  
EXPORT <object type> <object name>[, <object name>] [<object type> <object name>[, <object name] ] TO <filename> [WITH DEPENDENCIES]  
```  
  
## <a name="arguments"></a>引數  
 *物件類型*  
 選擇項。要匯出之物件的類型（不論是 [採礦模型] 或 [採礦結構]）。  
  
 *物件名稱*  
 選擇性。 要匯出的物件名稱。  
  
 *名稱*  
 要當成字串匯出之檔案的名稱和位置。  
  
## <a name="remarks"></a>備註  
 如果陳述式指定採礦模型，產生的檔案也會包含相關聯的採礦結構。 如果語句指定**WITH**相依性，則處理物件所需的所有物件（例如，資料來源和資料來源 view）都會包含在 .abf 檔案中。  
  
 您必須是資料庫或伺服器管理員，才能從[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]資料庫匯出或匯入物件。  
  
## <a name="export-mining-structure-example"></a>匯出採礦結構範例  
 下列範例會將 Targeted Mailing 與 Forecasting 採礦結構，以及 Association 採礦模型匯出到特定的檔案位置。 因為 Association 模型是 Market Basket 採礦結構的一部份，所以範例也會匯出 Market Basket 結構。 因為關聯模型是使用「**採礦模型**」（而非「**採礦結構**」）匯出，所以不會匯出任何可能當做購物籃採礦結構一部分存在的任何其他採礦模型。  
  
```  
EXPORT MINING STRUCTURE [Targeted Mailing], [Forecasting] MINING MODEL Association TO 'C:\TM_NEW.abf'  
```  
  
## <a name="export-mining-model-example"></a>匯出採礦模型範例  
 下列範例會將 Association 採礦模型匯出至指定的檔案位置。 由於語句會指定**WITH**相依性，因此資料來源和資料來源 view 物件也會包含在 .abf 檔案中。  
  
```  
EXPORT MINING MODEL [Association] TO 'C:\Association_NEW.abf' WITH DEPENDENCIES  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40;DMX&#41; 資料定義語句](../dmx/dmx-statements-data-definition.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 資料動作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語句參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [匯入 &#40;DMX&#41;](../dmx/import-dmx.md)   
 [匯出及匯入資料採礦物件](https://docs.microsoft.com/analysis-services/data-mining/export-and-import-data-mining-objects)  
  
  
