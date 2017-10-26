---
title: "匯入 (DMX) |Microsoft 文件"
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
- IMPORT
dev_langs:
- DMX
helpviewer_keywords:
- IMPORT statement
- mining structures [DMX], importing
ms.assetid: c053bc88-2daf-4ebb-81d7-5a330250536d
caps.latest.revision: 42
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 5510631430ed75a04dd9685d1197f60c64a85aa8
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="import-dmx"></a>IMPORT (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從 Analysis Services 備份檔案 (.abf) 中將採礦模型或採礦結構載入到伺服器。  
  
## <a name="syntax"></a>語法  
  
```  
  
IMPORT FROM <filename>  
```  
  
## <a name="arguments"></a>引數  
 *檔名*  
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
 [資料採礦延伸模組 &#40; DMX &#41;資料定義陳述式](../dmx/dmx-statements-data-definition.md)   
 [資料採礦延伸模組 &#40; DMX &#41;資料操作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40; DMX &#41;陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)   
 [匯出 &#40; DMX &#41;](../dmx/export-dmx.md)   
 [匯出和匯入資料採礦物件](../analysis-services/data-mining/export-and-import-data-mining-objects.md)  
  
  

