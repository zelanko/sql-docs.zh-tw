---
title: "VarP 函數 （報表產生器及 SSRS） |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e4f86ab3-bdb3-4e4a-9a9d-7ae7abdf4dc4
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 5fdfdc6df92afe9e150874d0dc1b1e99db29d0d7
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="report-builder-functions---varp-function"></a>報表產生器函式-VarP 函數
  傳回運算式指定的所有非 Null 數值的母體擴展變異數 (在給定範圍的內容中評估)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>語法  
  
```  
  
VarP(expression, scope, recursive)  
```  
  
#### <a name="parameters"></a>參數  
 *expression*  
 (**整數** 或 **浮點數**) 要在其上執行彙總的運算式。  
  
 *範圍 (scope)*  
 (**字串**) 選擇性。 包含要套用彙總函式之報表項目的資料集、群組或資料區的名稱。 如果未指定 *scope* ，則使用目前的範圍。  
  
 *遞迴*  
 (**列舉類型**) 選擇性。 **簡單** (預設值) 或 **RdlRecursive**。 指定是否要以遞迴方式執行彙總。  
  
## <a name="return-type"></a>傳回類型  
 十進位運算式會傳回 **Decimal** ，所有其他運算式都會傳回 **Double** 。  
  
## <a name="remarks"></a>備註  
 運算式中指定的資料集必須具有相同的資料類型。 若要將具有多個數值資料類型的資料轉換成相同的資料類型，請使用 **CInt**、 **CDbl** 或 **CDec**等轉換函數。 如需詳細資訊，請參閱 [類型轉換函數](http://go.microsoft.com/fwlink/?LinkId=96142)。  
  
 *scope* 的值必須是字串常數，而且不得為運算式。 如果是未指定其他彙總的外部彙總， *scope* 必須參考目前的範圍或是包含的範圍。 如果是彙總的彙總，巢狀彙總可以指定子範圍。  
  
 *Expression* 可以包含巢狀彙總函式的呼叫，其中包含下列例外和條件：  
  
-   巢狀彙總的*Scope* 必須與外部彙總的範圍相同或是由外部彙總的範圍所限制。 如果是運算式中的所有相異範圍，一個範圍必須與所有其他範圍之間具有子關聯性。  
  
-   巢狀彙總的*Scope* 不得為資料集的名稱。  
  
-   *Expression* 不得包含 **First**、 **Last**、 **Previous**或 **RunningValue** 函數。  
  
-   *Expression* 不得包含指定 *recursive*的巢狀彙總。  
  
 如需詳細資訊，請參閱[彙總函式參考 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) 和[總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
 如需遞迴彙總的詳細資訊，請參閱[建立遞迴階層群組 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)。  
  
## <a name="example"></a>範例  
 下列程式碼範例提供 `Order` 群組或資料區域中之行項目總計的母體擴展變異數。  
  
```  
=VarP(Fields!LineTotal.Value, "Order")  
```  
  
## <a name="see-also"></a>請參閱＜  
 [報表中的運算式用法 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [運算式範例 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [運算式中的資料類型 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [總計、彙總與內建集合的運算式範圍 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
