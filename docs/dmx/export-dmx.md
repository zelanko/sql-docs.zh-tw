---
title: "匯出 (DMX) |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- EXPORT
dev_langs:
- DMX
helpviewer_keywords:
- exporting mining models
- exporting mining structures
- mining structures [DMX], exporting
- EXPORT statement
ms.assetid: 97617071-e560-4080-81af-a80276fc0823
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: bfc3e8344d1c6967185979c0970be6d49b572500
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="export-dmx"></a>EXPORT (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從伺服器中將採礦模型或採礦結構物件擷取到 Analysis Services 備份檔案 (.abf)。  
  
## <a name="syntax"></a>語法  
  
```  
  
EXPORT <object type> <object name>[, <object name>] [<object type> <object name>[, <object name] ] TO <filename> [WITH DEPENDENCIES]  
```  
  
## <a name="arguments"></a>引數  
 *物件類型*  
 選用要匯出 （採礦模型或採礦結構） 的物件類型。  
  
 *物件名稱*  
 選擇性。 要匯出的物件名稱。  
  
 *檔名*  
 要當成字串匯出之檔案的名稱和位置。  
  
## <a name="remarks"></a>備註  
 如果陳述式指定採礦模型，產生的檔案也會包含相關聯的採礦結構。 如果陳述式指定**具有 WITH DEPENDENCIES**，處理物件 （例如，資料來源和資料來源檢視） 所需的所有物件都會都包含在.abf 檔案。  
  
 您必須是資料庫或伺服器管理員匯出或匯入物件從[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]資料庫。  
  
## <a name="export-mining-structure-example"></a>匯出採礦結構範例  
 下列範例會將 Targeted Mailing 與 Forecasting 採礦結構，以及 Association 採礦模型匯出到特定的檔案位置。 因為 Association 模型是 Market Basket 採礦結構的一部份，所以範例也會匯出 Market Basket 結構。 將不會匯出 Market Basket 採礦結構的一部分，因為 Association 模型使用匯出可能有的任何其他採礦模型**採礦模型**，而非**採礦結構**。  
  
```  
EXPORT MINING STRUCTURE [Targeted Mailing], [Forecasting] MINING MODEL Association TO 'C:\TM_NEW.abf'  
```  
  
## <a name="export-mining-model-example"></a>匯出採礦模型範例  
 下列範例會將 Association 採礦模型匯出至指定的檔案位置。 因為此陳述式指定**具有 WITH DEPENDENCIES**，資料來源和資料來源檢視物件也包含在.abf 檔案。  
  
```  
EXPORT MINING MODEL [Association] TO 'C:\Association_NEW.abf' WITH DEPENDENCIES  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40; DMX &#41;資料定義陳述式](../dmx/dmx-statements-data-definition.md)   
 [資料採礦延伸模組 &#40; DMX &#41;資料操作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40; DMX &#41;陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [匯入 &#40; DMX &#41;](../dmx/import-dmx.md)   
 [匯出和匯入資料採礦物件](../analysis-services/data-mining/export-and-import-data-mining-objects.md)  
  
  

