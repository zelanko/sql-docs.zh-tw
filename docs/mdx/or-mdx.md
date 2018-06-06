---
title: 或者 (MDX) |Microsoft 文件
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 215ed38ef7887d9815c6cf4ac79321b95a367707
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/02/2018
ms.locfileid: "34580620"
---
# <a name="or-mdx"></a>OR (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  在兩個數值運算式上執行邏輯分離。  
  
## <a name="syntax"></a>語法  
  
```  
  
Expression1 OR Expression2   
```  
  
#### <a name="parameters"></a>參數  
 Expression1  
 傳回數值的有效多維度運算式 (MDX) 運算式。  
  
 Expression2  
 傳回數值的有效 MDX 運算式。  
  
## <a name="return-value"></a>傳回值  
 布林值，傳回**true**如果任一個或兩個引數都評估為**true**，否則**false**。  
  
## <a name="remarks"></a>備註  
 **或者**運算子將兩個引數視為布林值 (零 （0) 做為**false**，否則**true**) 運算子執行邏輯分離之前。 下表將說明如何**或**運算子執行邏輯分離。  
  
|*Expression1*|*Expression2*|傳回值|  
|-------------------|-------------------|------------------|  
|**true**|**true**|**true**|  
|**true**|**false**|**true**|  
|**false**|**true**|**true**|  
|**false**|**false**|**false**|  
  
## <a name="example"></a>範例  
 如果 Customer 維度 Gender 階層上的目前成員為 Male，或者 Customer 維度 Marital Status 階層上的目前成員為 Married，下列包含導出量值的查詢會傳回字串 "MARRIED OR MALE"，否則會傳回字串 "UNMARRIED OR FEMALE"。  
  
```  
WITH  
MEMBER MEASURES.ORDEMO AS  
IIF(  
([Customer].[Gender].CURRENTMEMBER IS [Customer].[Gender].&[M])  
OR  
([Customer].[Marital Status].CURRENTMEMBER IS [Customer].[Marital Status].&[M]),  
"MARRIED OR MALE",  
"UNMARRIED OR FEMALE")  
SELECT [Customer].[Gender].[Gender].MEMBERS ON 0,  
[Customer].[Marital Status].[Marital Status].MEMBERS ON 1  
FROM [Adventure Works]  
WHERE(MEASURES.ORDEMO)  
```  
  
## <a name="see-also"></a>另請參閱  
 [MDX 運算子參考&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
