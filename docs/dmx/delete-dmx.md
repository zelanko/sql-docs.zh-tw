---
title: "刪除 (DMX) |Microsoft 文件"
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
- DELETE
dev_langs:
- DMX
helpviewer_keywords:
- DELETE statement [DMX]
- mining structures [DMX], clearing
- clearing mining models
- deleting mining models
- mining models [Analysis Services], clearing
- deleting mining structures
ms.assetid: 5a8204c3-a3df-4d97-9c1d-d997d24c70e3
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 00be9b52e652e2a2456cdbcd589f048d8a971d47
ms.contentlocale: zh-tw
ms.lasthandoff: 08/02/2017

---
# <a name="delete-dmx"></a>DELETE (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  根據您使用的資料採礦延伸模組 (DMX) 子句，清除採礦模型、採礦結構，或採礦結構及其所有相關聯的採礦模型。  
  
## <a name="syntax"></a>語法  
  
```  
  
DELETE FROM [MINING MODEL] <model>[.CONTENT]  
DELETE FROM [MINING STRUCTURE] <structure>[.CONTENT]|[.CASES]  
```  
  
## <a name="arguments"></a>引數  
 *model*  
 模型識別碼。  
  
 *結構*  
 結構識別碼。  
  
## <a name="remarks"></a>備註  
 如果您未指定**採礦模型**或**採礦結構**，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]搜尋名稱為基礎的物件類型，並處理正確的物件。 如果伺服器包含具有相同名稱的採礦結構與採礦模型，就會傳回錯誤。  
  
 下表說明使用不同語法格式的結果。  
  
|引數|結果|  
|---------------|------------|  
|DELETE FROM MINING STRUCTURE*\<結構 >*<br /><br /> 或<br /><br /> DELETE FROM MINING STRUCTURE*\<結構 >*。內容|在採礦結構上執行 ProcessClear。 清除採礦結構及其相關聯的採礦模型中所有的內容。|  
|DELETE FROM MINING STRUCTURE*\<結構 >*。案例|在採礦結構上執行 ProcessClearStructureOnly。 清除採礦結構中所有的內容，但是相關聯的採礦模型則保持不變。 清除採礦結構之後，在相關聯之採礦模型上的鑽研將會失敗。|  
|從採礦模型 刪除*\<模型 >*<br /><br /> 或<br /><br /> 從採礦模型 刪除*\<模型 >*。內容|採礦模型上執行 ProcessClear，但會保留資料庫中的狀態值。 狀態值是資料行的可能狀態。 例如，性別資料行的狀態值為男性與女性。|  
  
 如需有關處理類型的詳細資訊，請參閱[Type 元素 &#40;XMLA &#41;](../analysis-services/xmla/xml-elements-properties/type-element-xmla.md).  
  
## <a name="examples"></a>範例  
 下列範例會移除 NB_Sample 模型中的所有內容。  
  
```  
DELETE FROM NB_Sample.CONTENT  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組 &#40; DMX &#41;資料定義陳述式](../dmx/dmx-statements-data-definition.md)   
 [資料採礦延伸模組 &#40; DMX &#41;資料操作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40; DMX &#41;陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)  
  
  

