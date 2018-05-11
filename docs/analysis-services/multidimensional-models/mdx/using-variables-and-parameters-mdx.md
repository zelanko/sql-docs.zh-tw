---
title: 使用變數和參數 (MDX) |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5ba2f11d786811eeb108c57d3d8336e3da541593
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="using-variables-and-parameters-mdx"></a>使用變數與參數 (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中，您可以參數化多維度運算式 (MDX) 陳述式。 您可以使用參數化陳述式，建立可在執行階段自訂的一般陳述式。  
  
 在建立參數化陳述式時，您可以在名稱前面加上 @ 符號，來識別參數名稱。 例如，@Year會是有效的參數名稱  
  
 MDX 只支援常值或純量值的參數。 若要建立參考成員、集合或 Tuple 的參數，您必須使用函數，例如 [StrToMember](../../../mdx/strtomember-mdx.md) 或 [StrToSet](../../../mdx/strtoset-mdx.md)。  
  
 下列 XML for Analysis (XMLA) 範例中@CountryName參數會包含國家/地區的客戶擷取資料：  
  
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
  
 此功能若要與 OLE DB 搭配使用，您可以使用 **ICommandWithParameters** 介面。 此功能若要與 ADOMD.Net 搭配使用，您可以使用 **AdomdCommand.Parameters** 集合。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 指令碼基礎觀念 & #40;Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)  
  
  
