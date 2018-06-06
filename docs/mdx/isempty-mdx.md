---
title: IsEmpty (MDX) |Microsoft 文件
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ab2f65bbc15aecec93294225435d3d2d38fff062
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34578710"
---
# <a name="isempty-mdx"></a>IsEmpty (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  傳回評估的運算式是否為空白資料格值。  
  
## <a name="syntax"></a>語法  
  
```  
  
IsEmpty(Value_Expression)   
```  
  
## <a name="arguments"></a>引數  
 *Value_Expression*  
 一般會傳回成員或 Tuple 之資料格座標的有效多維度運算式 (MDX) 運算式。  
  
## <a name="remarks"></a>備註  
 **IsEmpty**函式會傳回**true**如果評估的運算式是空的資料格的值。 否則，此函數會傳回**false**。  
  
> [!NOTE]  
>  成員的預設屬性就是成員的值。  
  
 **IsEmpty**函式是唯一能確實地測試空白資料格的空白資料格值具有特殊意義，因為[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。  
  
> [!IMPORTANT]  
>  如果值運算式的評估會傳回錯誤，此函數會傳回**false**。 例如，屬性參考所參考的是無效或不存在的屬性時，值運算式會傳回錯誤。  
  
 如需有關空的資料格的詳細資訊，請參閱 OLE DB 文件集。  
  
## <a name="example"></a>範例  
 如果 Date 維度 Fiscal 階層上目前成員的 Internet Sales Amount 傳回空資料格，下列範例會傳回 TRUE：  
  
 `WITH MEMBER MEASURES.ISEMPTYDEMO AS`  
  
 `IsEmpty([Measures].[Internet Sales Amount])`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.ISEMPTYDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另請參閱  
 [使用空白值](../mdx/working-with-empty-values.md)   
 [MDX 函數參考&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
