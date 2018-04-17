---
title: 使用預存程序 (MDX) |Microsoft 文件
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- user-defined functions [MDX]
- stored procedures [MDX]
ms.assetid: 818fb2ad-f88b-4d0c-9f70-f378aed42e8e
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: e591f000488220b9d1db784c39b82a991837401d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="using-stored-procedures-mdx"></a>使用預存程序 (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
>  *預存程序*是中使用的術語[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]這些類型的函式。 舊版的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]呼叫這些類型的函式做為*使用者定義函數*。  
  
## <a name="types-of-stored-procedures"></a>預存程序類型  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 支援 COM 及 CLR 兩種組件。 因為 CLR 組件具備進階的安全性，所以建議使用 CLR 組件。 如果伺服器上已安裝 Microsoft Office Excel，還可以使用 Excel 函數。  
  
> [!NOTE]  
>  Microsoft Visual Basic for Applications (VBA) COM 組件會自動註冊。  
  
## <a name="see-also"></a>請參閱  
 [函式 &#40;MDX 語法 &#41;](../mdx/functions-mdx-syntax.md)  
  
  
