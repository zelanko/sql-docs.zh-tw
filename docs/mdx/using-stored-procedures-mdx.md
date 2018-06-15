---
title: 使用預存程序 (MDX) |Microsoft 文件
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2a0ba1b350e59406f04796924385059c323facd6
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34743797"
---
# <a name="using-stored-procedures-mdx"></a>使用預存程序 (MDX)


  您可以擴充 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 和多維度運算式 (MDX) 的功能，其方式是撰寫 .NET 預存程序或使用者定義函數。 如需詳細資訊，請參閱[ADOMD.NET 伺服器程式設計](../analysis-services/multidimensional-models-adomd-net-server/adomd-net-server-programming.md)  
  
 當您要參考或呼叫預存程序時，必須指定函數的名稱，並在後面加上括號。 您可以在括號中指定稱為引數的運算式，它會提供要傳送給參數的資料。 當您呼叫函數時，必須提供所有參數的引數值，而指定引數值的順序必須跟使用者自訂函數中定義參數的順序相同。  
  
 下列範例查詢假設您在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 伺服器上已註冊一個名為 SampleAssembly 的組件：  
  
```  
SELECT SampleAssembly.RandomSample([Geography].[State-Province].Members, 5) on ROWS,   
[Date].[Calendar].[Calendar Year] on COLUMNS  
FROM [Adventure Works]  
WHERE [Measures].[Reseller Freight Cost]  
```  
  
> [!NOTE]  
>  *預存程序*是中使用的術語[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]這些類型的函式。 舊版的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]呼叫這些類型的函式做為*使用者定義函數*。  
  
## <a name="types-of-stored-procedures"></a>預存程序類型  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 支援 COM 及 CLR 兩種組件。 因為 CLR 組件具備進階的安全性，所以建議使用 CLR 組件。 如果伺服器上已安裝 Microsoft Office Excel，還可以使用 Excel 函數。  
  
> [!NOTE]  
>  Microsoft Visual Basic for Applications (VBA) COM 組件會自動註冊。  
  
## <a name="see-also"></a>另請參閱  
 [函式&#40;MDX 語法&#41;](../mdx/functions-mdx-syntax.md)  
  
  
