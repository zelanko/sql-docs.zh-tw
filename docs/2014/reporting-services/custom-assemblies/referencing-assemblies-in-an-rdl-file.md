---
title: 參考在 RDL 檔案中的組件 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- RDL [Reporting Services], referencing assemblies
- referencing custom assemblies
- custom assemblies [Reporting Services], referencing
- Report Definition Language, referencing assemblies
- report definition files [Reporting Services]
ms.assetid: 9a48e552-7d47-4243-9be1-894990c506d9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bc52419f382ea44fc718a47e99bbd0981275d240
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63264801"
---
# <a name="referencing-assemblies-in-an-rdl-file"></a>參考在 RDL 檔案中的組件
  為了支援報表定義檔案中自訂程式碼組件的用法，在 RDL 規格中加入了兩個報表定義語言 (RDL) 項目：**CodeModules** 項目與 **Classes** 項目。  
  
 **CodeModules** 項目可讓您參考報表運算式中的 Managed 程式碼組件。 **CodeModules** 是最上層的項目，包含在報表定義檔案中用以呼叫特定函式的組件參考。 支援自訂組件用法的報表定義中的項目可能如下所示：  
  
```  
<CodeModules>  
   <CodeModule>CurrencyConversion, Version=1.0.1363.31103, Culture=neutral, PublicKeyToken=null</CodeModule>  
</CodeModules>  
```  
  
 請不要從自訂程式碼呼叫 <xref:System.Reflection.Assembly.Load%2A>，而是透過將 **CodeModule** 項目手動新增至 RDL 檔案，或是透過使用 [報表屬性] 對話方塊的 [參考] 索引標籤來註冊自訂組件。 如需詳細資訊，請參閱 [報表設計師中運算式的自訂程式碼及組件參考 &#40;SSRS&#41;](../report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)。  
  
 **Classes** 項目支援在報表定義中使用執行個體成員。 **Classes** 是最上層項目，包含類別名稱與執行個體名稱的參考。 支援使用執行個體成員之報表定義中的項目可能如下所示：  
  
```  
<Classes>  
   <Class>  
      <ClassName>CurrencyConversion.DollarCurrencyConversion</ClassName>  
      <InstanceName>m_myDollarConversion</InstanceName>  
   </Class>  
</Classes>  
```  
  
 如需詳細資訊，請參閱[透過運算式存取自訂組件](accessing-custom-assemblies-through-expressions.md)。  
  
## <a name="see-also"></a>另請參閱  
 [將自訂組件與報表搭配使用](using-custom-assemblies-with-reports.md)  
  
  
