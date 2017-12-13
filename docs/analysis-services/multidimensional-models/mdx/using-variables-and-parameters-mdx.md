---
title: "使用變數和參數 (MDX) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- parameters [MDX]
- queries [MDX], variables
- queries [MDX], parameters
- variables [MDX]
ms.assetid: a4754d16-d9c4-49f6-9be0-392180b912e4
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0fab0f7b78e89048d0a953490683740960cb4ab4
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="using-variables-and-parameters-mdx"></a>使用變數與參數 (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]在[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，您可以參數化多維度運算式 (MDX) 陳述式。 您可以使用參數化陳述式，建立可在執行階段自訂的一般陳述式。  
  
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
  
## <a name="see-also"></a>請參閱  
 [MDX 指令碼基礎觀念 &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)  
  
  
