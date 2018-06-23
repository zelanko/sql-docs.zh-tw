---
title: 使用變數和參數 (MDX) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- parameters [MDX]
- queries [MDX], variables
- queries [MDX], parameters
- variables [MDX]
ms.assetid: a4754d16-d9c4-49f6-9be0-392180b912e4
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: a2e477c1faa1f8bed7568c510418abb006875f48
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032180"
---
# <a name="using-variables-and-parameters-mdx"></a>使用變數與參數 (MDX)
  在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中，您可以參數化多維度運算式 (MDX) 陳述式。 您可以使用參數化陳述式，建立可在執行階段自訂的一般陳述式。  
  
 在建立參數化陳述式時，您可以在名稱前面加上 @ 符號，來識別參數名稱。 例如，@Year會是有效的參數名稱  
  
 MDX 只支援常值或純量值的參數。 若要建立參考成員、集合或 Tuple 的參數，您必須使用函數，例如 [StrToMember](/sql/mdx/strtomember-mdx) 或 [StrToSet](/sql/mdx/strtoset-mdx)。  
  
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
  
 若要使用 OLE DB 中使用這項功能，您可以使用`ICommandWithParameters`介面。 此功能若要與 ADOMD.Net 搭配使用，您可以使用 **AdomdCommand.Parameters** 集合。  
  
## <a name="see-also"></a>另請參閱  
 [MDX 指令碼基礎觀念&#40;Analysis Services&#41;](mdx-scripting-fundamentals-analysis-services.md)  
  
  
