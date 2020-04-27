---
title: 混合的類型與簡單的內容 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- mixed types [SQL Server]
ms.assetid: 6ea1f11d-e64b-4ebb-ab68-4eb6e4027665
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cf0e4f54334d84aea5a33392655110374e893cc4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63241273"
---
# <a name="mixed-type-and-simple-content"></a>混合的類型與簡單的內容
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援將混合類型限制為簡單內容。  
  
## <a name="example"></a>範例  
 在下列 XML 結構描述集合中， `myComplexTypeA` 是可以清空的複雜類型。 也就是說，它的兩個元素都會將 `minOccurs` 設定為 0。 不支援透過在 `myComplexTypeB` 宣告中的方式，將此限制為簡單內容。 因此，下列 XML 結構描述集合的建立將會失敗：  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="http://ns" xmlns:ns="http://ns"  
xmlns:ns1="http://ns1">  
  
    <complexType name="myComplexTypeA" mixed="true">  
        <sequence>  
            <element name="a" type="string" minOccurs="0"/>  
            <element name="b" type="string" minOccurs="0" maxOccurs="23"/>  
        </sequence>  
    </complexType>  
  
    <complexType name="myComplexTypeB">  
        <simpleContent>  
            <restriction base="ns:myComplexTypeA">  
                <simpleType>  
                    <restriction base="int">  
                        <minExclusive value="25"/>  
                    </restriction>  
                </simpleType>  
            </restriction>  
        </simpleContent>  
    </complexType>  
</schema>  
'  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [伺服器上 XML 結構描述集合的需求與限制](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
