---
title: "參考在 RDL 檔案中的組件 |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- RDL [Reporting Services], referencing assemblies
- referencing custom assemblies
- custom assemblies [Reporting Services], referencing
- Report Definition Language, referencing assemblies
- report definition files [Reporting Services]
ms.assetid: 9a48e552-7d47-4243-9be1-894990c506d9
caps.latest.revision: 36
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 87609ab5b118eaa696f7152b25cf7e984e7f6e7f
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="referencing-assemblies-in-an-rdl-file"></a>參考在 RDL 檔案中的組件
  若要支援使用自訂程式碼組件的報表定義檔案中，兩個報表定義語言 (RDL) 元素會包含在 RDL 規格： **CodeModules**項目和**類別**項目。  
  
 **CodeModules**項目可讓您在報表運算式中的 managed 程式碼組件參考。 **CodeModules**是最上層的元素，其中包含您在報表定義檔案中用來呼叫特定的函數的組件的參考。 支援自訂組件用法的報表定義中的項目可能如下所示：  
  
```  
<CodeModules>  
   <CodeModule>CurrencyConversion, Version=1.0.1363.31103, Culture=neutral, PublicKeyToken=null</CodeModule>  
</CodeModules>  
```  
  
 而不是呼叫<xref:System.Reflection.Assembly.Load%2A>從自訂程式碼，請手動加入，自訂組件註冊**CodeModule** RDL 檔案，或使用的項目**參考** 索引標籤**報表屬性**對話方塊。 如需詳細資訊，請參閱 [報表設計師中運算式的自訂程式碼及組件參考 &#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)。  
  
 **類別**項目支援報表定義中使用的執行個體成員。 **類別**是最上層的元素，其中包含的類別名稱和執行個體名稱的參考。 支援使用執行個體成員之報表定義中的項目可能如下所示：  
  
```  
<Classes>  
   <Class>  
      <ClassName>CurrencyConversion.DollarCurrencyConversion</ClassName>  
      <InstanceName>m_myDollarConversion</InstanceName>  
   </Class>  
</Classes>  
```  
  
 如需詳細資訊，請參閱[存取 Custom Assemblies Through Expressions](../../reporting-services/custom-assemblies/accessing-custom-assemblies-through-expressions.md)。  
  
## <a name="see-also"></a>另請參閱  
 [報表中使用自訂組件](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
