---
title: 預設包含 NULL 值的資料行 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- columns [XML in SQL Server], null default value
ms.assetid: 9381c07f-6887-4a62-9730-32661f9aa87c
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3aaa7cc6fb40c2f600e734cb3e2250a40e15d63e
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717295"
---
# <a name="columns-that-contain-a-null-value-by-default"></a>預設包含 NULL 值的資料行
  依預設，資料行中的 Null 值會與缺少的屬性、節點或元素相對應。 此預設行為是可以覆寫的，方法為使用 ELEMENTS 指示詞來要求元素中心的 XML，並指定 XSINIL 來要求為 NULL 值加入元素，如下列查詢所示：  
  
```  
SELECT EmployeeID as "@EmpID",   
       FirstName  as "EmpName/First",   
       MiddleName as "EmpName/Middle",   
       LastName   as "EmpName/Last"  
FROM   HumanResources.Employee E, Person.Contact C  
WHERE  E.EmployeeID = C.ContactID  
AND    E.EmployeeID=1  
FOR XML PATH, ELEMENTS XSINIL  
```  
  
 下列範例會顯示結果。 請注意如果沒有指定 XSINIL，將不會有 <`Middle`> 元素。  
  
```  
<row xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Middle xsi:nil="true" />  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
## <a name="see-also"></a>另請參閱  
 [搭配 FOR XML 使用 PATH 模式](use-path-mode-with-for-xml.md)  
  
  
