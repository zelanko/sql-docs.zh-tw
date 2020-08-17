---
description: IMPORT (DMX)
title: 匯入 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5da00163792b18bfd62ed0db4be0945f358115e3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88352684"
---
# <a name="import-dmx"></a>IMPORT (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  從 Analysis Services 備份檔案 (.abf) 中將採礦模型或採礦結構載入到伺服器。  
  
## <a name="syntax"></a>語法  
  
```  
  
IMPORT FROM <filename>  
```  
  
## <a name="arguments"></a>引數  
 *filename*  
 包含要匯入檔案之名稱與位置的字串。  
  
## <a name="remarks"></a>備註  
 如果未指定物件，則會載入 .dmb 檔案的全部內容。 如果 .dmb 檔案包含的資料庫不存在伺服器上，則會建立資料庫。  
  
 您必須是資料庫或伺服器管理員，才能匯出或匯入物件。  
  
## <a name="import-from-file-example"></a>從檔案匯入的範例  
 下列範例會將包含關聯模型和結構之檔案的完整內容匯入目前的伺服器。  
  
```  
IMPORT FROM 'C:\TEMP\Association_NEW.dmb'  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40;DMX&#41; 資料定義語句](../dmx/dmx-statements-data-definition.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 資料動作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 語句參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [匯出 &#40;DMX&#41;](../dmx/export-dmx.md)   
 [匯出及匯入資料採礦物件](https://docs.microsoft.com/analysis-services/data-mining/export-and-import-data-mining-objects)  
  
  
