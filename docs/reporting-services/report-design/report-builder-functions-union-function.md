---
title: Union 函式 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c87e16fe-c12a-4c9d-a9df-7a94e229fd04
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f7098f2407a15828a9b12e5e0ca0b0f26bb57883
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33025985"
---
# <a name="report-builder-functions---union-function"></a>報表產生器函式 - Union 函式
  傳回運算式所指定之所有非 Null 數值的聯集 (在給定範圍中評估)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>語法  
  
```  
  
Union(expression, scope, recursive)  
```  
  
#### <a name="parameters"></a>參數  
 *expression*  
 (**SqlGeometry** 或 **SqlGeography**) 要在其上執行彙總的運算式。  
  
 *範圍 (scope)*  
 (**字串**) 選擇性。 包含要套用彙總函式之報表項目的資料集、群組或資料區的名稱。 如果未指定 *scope* ，則使用目前的範圍。  
  
 *遞迴*  
 (**列舉型別**) 選擇性。 **簡單** (預設值) 或 **RdlRecursive**。 指定是否要以遞迴方式執行彙總。  
  
## <a name="return"></a>傳回  
 根據運算式類型傳回空間物件 ( **SqlGeometry** 或 **SqlGeography**)。 如需 **SqlGeometry** 和 **SqlGeography** 空間資料類型的詳細資訊，請參閱 [空間資料類型概觀](../../relational-databases/spatial/spatial-data-types-overview.md)。  
  
## <a name="remarks"></a>Remarks  
 運算式中指定的資料集必須具有相同的資料類型。  
  
 *scope* 的值必須是字串常數，而且不得為運算式。 如果是未指定其他彙總的外部彙總， *scope* 必須參考目前的範圍或是包含的範圍。 不支援資料集範圍。 如果是彙總的彙總，巢狀彙總可以指定子範圍。  
  
 *Expression* 可以包含巢狀彙總函式的呼叫，其中包含下列例外和條件：  
  
-   巢狀彙總的*Scope* 必須與外部彙總的範圍相同或是由外部彙總的範圍所限制。 如果是運算式中的所有相異範圍，一個範圍必須與所有其他範圍之間具有子關聯性。  
  
-   巢狀彙總的*Scope* 不得為資料集的名稱。  
  
-   *Expression* 不得包含 **First**、 **Last**、 **Previous**或 **RunningValue** 函數。  
  
-   *Expression* 不得包含指定 *recursive*的巢狀彙總。  
  
 如需詳細資訊，請參閱[彙總函式參考 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) 和[總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
 如需遞迴彙總的詳細資訊，請參閱[建立遞迴階層群組 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)。  
  
## <a name="example"></a>範例  
 下表顯示 **SqlGeometry** 運算式和 **Union** 果運算式的範例，使用適用於空間資料的 WKT (已知文字) 格式顯示。  
  
|具有空間資料的欄位|範例|聯集結果|  
|-----------------------------|-------------|------------------|  
|[PointLocation]|POINT(1 2)<br /><br /> POINT(3 4)|MULTIPOINT((1 2), (3 4))|  
|[PathDefinition]|LINESTRING(1 2, 3 4)<br /><br /> LINESTRING(5 6, 7 8)|MULTILINESTRING((7 8, 5 6), (3 4, 1 2))|  
|[PolygonDefinition]|POLYGON((1 2, 3 4, 5 2, 1 2))<br /><br /> POLYGON((-1 2, -3 4, -5 2, -1 2))|MULTIPOLYGON(((1 2, 5 2, 3 4, 1 2)), ((-5 2, -1 2, -3 4, -5 2)))|  
  
```  
=Union(Fields!PointLocation.Value)  
=Union(Fields!PathDefinition.Value)  
=Union(Fields!PolygonDefinition.Value, "Group1")  
```  
  
## <a name="see-also"></a>另請參閱  
 [報表中的運算式用法 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
