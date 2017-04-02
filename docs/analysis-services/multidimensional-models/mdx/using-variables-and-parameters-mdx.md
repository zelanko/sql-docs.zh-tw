---
title: "使用變數與參數 (MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "參數 [MDX]"
  - "查詢 [MDX], 變數"
  - "查詢 [MDX], 參數"
  - "變數 [MDX]"
ms.assetid: a4754d16-d9c4-49f6-9be0-392180b912e4
caps.latest.revision: 29
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 29
---
# 使用變數與參數 (MDX)
  在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中，您可以參數化多維度運算式 (MDX) 陳述式。 您可以使用參數化陳述式，建立可在執行階段自訂的一般陳述式。  
  
 在建立參數化陳述式時，您可以在名稱前面加上 @ 符號，來識別參數名稱。 例如，@Year 是個有效的參數名稱。  
  
 MDX 只支援常值或純量值的參數。 若要建立參考成員、集合或 Tuple 的參數，您必須使用函數，例如 [StrToMember](../../../mdx/strtomember-mdx.md) 或 [StrToSet](../../../mdx/strtoset-mdx.md)。  
  
 在以下 XML for Analysis (XMLA) 範例中，@CountryName 參數將會包含其客戶資料已予擷取的國家 (地區)：  
  
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
  
## 請參閱＜  
 [MDX 指令碼基礎觀念 &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)  
  
  