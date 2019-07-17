---
title: 刪除 (DMX) |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c1c75a6ff18b26bee65365acbc068de87678a9c7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070759"
---
# <a name="delete-dmx"></a>DELETE (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  根據您使用的資料採礦延伸模組 (DMX) 子句，清除採礦模型、採礦結構，或採礦結構及其所有相關聯的採礦模型。  
  
## <a name="syntax"></a>語法  
  
```  
  
DELETE FROM [MINING MODEL] <model>[.CONTENT]  
DELETE FROM [MINING STRUCTURE] <structure>[.CONTENT]|[.CASES]  
```  
  
## <a name="arguments"></a>引數  
 *model*  
 模型識別碼。  
  
 *structure*  
 結構識別碼。  
  
## <a name="remarks"></a>備註  
 如果您未指定**採礦模型**或是**採礦結構**，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]搜尋名稱，以基礎物件型別，並處理正確的物件。 如果伺服器包含具有相同名稱的採礦結構與採礦模型，就會傳回錯誤。  
  
 下表說明使用不同語法格式的結果。  
  
|陳述式|結果|  
|---------------|------------|  
|DELETE FROM MINING STRUCTURE *\<結構 >*<br /><br /> 或<br /><br /> DELETE FROM MINING STRUCTURE *\<結構 >* 。內容|在採礦結構上執行 ProcessClear。 清除採礦結構及其相關聯的採礦模型中所有的內容。|  
|DELETE FROM MINING STRUCTURE *\<結構 >* 。案例|在採礦結構上執行 ProcessClearStructureOnly。 清除採礦結構中所有的內容，但是相關聯的採礦模型則保持不變。 清除採礦結構之後，在相關聯之採礦模型上的鑽研將會失敗。|  
|刪除從採礦模型 *\<模型 >*<br /><br /> 或<br /><br /> 刪除從採礦模型 *\<模型 >* 。內容|在採礦模型上執行 ProcessClear，但會保留資料庫中的狀態值。 狀態值是資料行的可能狀態。 例如，性別資料行的狀態值為男性與女性。|  
  
 如需處理類型的詳細資訊，請參閱 <<c0> [ 型別項目&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/type-element-xmla)。</c0>  
  
## <a name="examples"></a>範例  
 下列範例會移除 NB_Sample 模型中的所有內容。  
  
```  
DELETE FROM NB_Sample.CONTENT  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料採礦延伸模組&#40;DMX&#41;資料定義陳述式](../dmx/dmx-statements-data-definition.md)   
 [資料採礦延伸模組&#40;DMX&#41;資料操作陳述式](../dmx/dmx-statements-data-manipulation.md)   
 [資料採礦延伸模組 &#40;DMX&#41; 陳述式參考](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
