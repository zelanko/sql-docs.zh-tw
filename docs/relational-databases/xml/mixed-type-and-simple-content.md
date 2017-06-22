---
title: "混合的類型與簡單的內容 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mixed types [SQL Server]
ms.assetid: 6ea1f11d-e64b-4ebb-ab68-4eb6e4027665
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4c6ca3595ced1ff8d74c625d25e507b246f84342
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

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
 [伺服器上 XML 結構描述集合的需求與限制](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
