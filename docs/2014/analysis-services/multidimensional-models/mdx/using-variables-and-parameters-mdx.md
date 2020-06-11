---
title: 使用變數和參數（MDX） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- parameters [MDX]
- queries [MDX], variables
- queries [MDX], parameters
- variables [MDX]
ms.assetid: a4754d16-d9c4-49f6-9be0-392180b912e4
author: minewiskan
ms.author: owend
ms.openlocfilehash: fd01cf78ea5e3284aa51cad7dc848176a5dc9298
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546150"
---
# <a name="using-variables-and-parameters-mdx"></a>使用變數與參數 (MDX)
  在中 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ，您可以參數化多維度運算式（MDX）語句。 您可以使用參數化陳述式，建立可在執行階段自訂的一般陳述式。  
  
 在建立參數化陳述式時，您可以在名稱前面加上 @ 符號，來識別參數名稱。 例如， @Year 會是有效的參數名稱  
  
 MDX 只支援常值或純量值的參數。 若要建立參考成員、集合或 Tuple 的參數，您必須使用函數，例如 [StrToMember](/sql/mdx/strtomember-mdx) 或 [StrToSet](/sql/mdx/strtoset-mdx)。  
  
 在下列 XML for Analysis （XMLA）範例中， @CountryName 參數會包含取得客戶資料的國家/地區：  
  
```  
<Envelope xmlns="http://schemas.xmlsoap.org/soap/envelope/">  
  <Body>  
    <Execute xmlns="urn:schemas-microsoft-com:xml-analysis">  
      <Command>  
        <Statement>  
select [Measures].members on 0,   
       Filter(Customer.[Customer Geography].Country.members,   
              Customer.[Customer Geography].CurrentMember.Name =  
              @CountryName) on 1  
from [Adventure Works]  
</Statement>  
      </Command>  
      <Properties />  
      <Parameters>  
        <Parameter>  
          <Name>CountryName</Name>  
          <Value>'United Kingdom'</Value>  
        </Parameter>  
      </Parameters>  
    </Execute>  
  </Body>  
</Envelope>  
```  
  
 若要將此功能與 OLE DB 搭配使用，您可以使用 `ICommandWithParameters` 介面。 此功能若要與 ADOMD.Net 搭配使用，您可以使用 **AdomdCommand.Parameters** 集合。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 指令碼基礎觀念 &#40;Analysis Services&#41;](mdx-scripting-fundamentals-analysis-services.md)  
  
  
