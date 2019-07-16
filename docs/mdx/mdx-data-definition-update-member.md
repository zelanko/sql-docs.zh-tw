---
title: UPDATE MEMBER 陳述式 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 73a2bf2973d8c4f8f9bf9ac886728fb45250343f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038142"
---
# <a name="mdx-data-definition---update-member"></a>MDX 資料定義 - UPDATE MEMBER


  更新現有導出成員。  
  
## <a name="syntax"></a>語法  
  
```  
  
UPDATE MEMBER Cube_Name.Member_Name   
   AS MDX_Expression  
      [,Property_Name = Property_Value, ...n]  
......[,SCOPE_ISOLATION = CUBE]  
```  
  
## <a name="arguments"></a>引數  
 *Cube_Name*  
 指定包含成員之 Cube 名稱的有效字串。  
  
 *Member_Name*  
 指定現有成員之名稱的有效字串。  
  
 *MDX_Expression*  
 要更新之成員的有效多維度運算式 (MDX) 運算式。  
  
 *Property_Name*  
 指定導出成員屬性名稱的有效字串。  
  
 *Property_Value*  
 指定導出成員屬性值的有效純量運算式。  
  
## <a name="remarks"></a>備註  
 UPDATE MEMBER 陳述式會在更新現有導出成員的同時，保留此成員對於其他計算的相對優先順序。 因此，您無法使用 UPDATE MEMBER 陳述式變更 SOLVEORDER。  
  
 在 Cube 的 MDX 指令碼中，無法指定 UPDATE MEMBER 陳述式。  
  
 指定目前連接之 Cube 以外的 Cube 會導致發生錯誤。 因此，您應該使用 CURRENTCUBE 取代 Cube 名稱，來代表目前的 Cube。  
  
 如需 OLE DB 定義之成員屬性的詳細資訊，請參閱 OLE DB 文件集。  
  
## <a name="standard-properties"></a>標準屬性  
 每個成員都有一組預設屬性。 下表列出這些預設屬性。  
  
|屬性識別碼|意義|  
|-------------------------|-------------|  
|FORMAT_STRING|Office 樣式格式字串，用戶端應用程式可用來顯示資料格的值。|  
|VISIBLE|指出是否可以看見結構描述資料列集中導出成員的值。 可見的導出成員可以加入至一組[AddCalculatedMembers](../mdx/addcalculatedmembers-mdx.md)函式。 非零的值代表可以看見導出成員。 這個屬性的預設值是*Visible*。<br /><br /> 不可見的導出成員一般會在較為複雜的導出成員中做為中間步驟。 其他成員類型 (例如，量值) 也可以參考這些導出成員。|  
|NON_EMPTY_BEHAVIOR|解析空白資料格時，MDX 用以決定導出成員行為的量值或集合。|  
|CAPTION|指定用戶端應用程式用於顯示成員之標題的字串值。|  
|DISPLAY_FOLDER|指定用戶端應用程式顯示之成員所在顯示資料夾路徑的字串值。 資料夾層級的分隔符號是由用戶端應用程式所定義。 工具和所提供的用戶端[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，反斜線 (\\) 為層級分隔符號。 若要針對已定義的成員提供多個顯示資料夾，請使用分號 (;) 來分隔資料夾。|  
|ASSOCIATED_MEASURE_GROUP|與此成員建立關聯之量值群組的名稱。|  
  
## <a name="see-also"></a>另請參閱  
 [DROP MEMBER 陳述式&#40;MDX&#41;](../mdx/mdx-data-definition-drop-member.md)   
 [CREATE MEMBER 陳述式 &#40;MDX&#41;](../mdx/mdx-data-definition-create-member.md)   
 [MDX 資料定義陳述式&#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
