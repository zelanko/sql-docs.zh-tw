---
title: 本機名稱-從 QName (XQuery) |Microsoft Docs
description: '瞭解如何使用本機名稱-從 QName ( # A1 函式來傳回 QName 的本機名稱部分。'
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:local-name-from-QName function
- local-name-from-QName function
ms.assetid: fafed718-8c3c-403f-93ee-ec51fc157a6e
author: rothja
ms.author: jroth
ms.openlocfilehash: d19153bbfd3cf2483cf8dfa30358f752dd45290e
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036811"
---
# <a name="functions-related-to-qnames---local-name-from-qname"></a>與 QNames 相關的函式 - local-name-from-QName
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

  傳回 xs： NCNAME，代表 *$arg*指定之 QName 的本機部分。 如果 *$arg* 是空的序列，則結果為空的序列。  
  
## <a name="syntax"></a>語法  
  
```  
fn:local-name-from-QName($arg as xs:QName?) as xs:NCName?  
```  
  
## <a name="arguments"></a>引數  
 *$arg*  
 應該擷取本機名稱的來源 QName。  
  
## <a name="examples"></a>範例  
 本主題針對 XML 實例提供 XQuery 範例，這些實例是儲存在資料庫的各種 **XML** 類型資料行中 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 。  
  
 下列範例會使用 **本機名稱-從 qname ( # B1 ** 函數，從 qname 類型值取出區功能變數名稱稱和命名空間 URI 部分。 本範例將執行下列動作：  
  
-   建立 XML 結構描述集合。  
  
-   建立資料表以及 xml 類型資料行。 xml 類型是使用 XML 結構描述集合來設定其類型。  
  
-   在資料表中儲存範例 XML 執行個體。 使用查詢 ( xml 資料類型的 **# B1 ** 方法時，會執行查詢運算式，以從實例中取出 QName 類型值的本機名稱部分。  
  
```sql
DROP TABLE T  
go  
DROP XML SCHEMA COLLECTION SC  
go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
targetNamespace="QNameXSD" >  
      <element name="root" type="QName" nillable="true"/>  
</schema>'  
go  
  
CREATE TABLE T (xmlCol XML(SC))  
go  
-- following OK  
insert into T values ('<root xmlns="QNameXSD" xmlns:a="https://someURI">a:someLocalName</root>')  
 go  
-- Retrieve the local name.   
SELECT xmlCol.query('declare default element namespace "QNameXSD"; local-name-from-QName(/root[1])')  
FROM T  
-- Result = someLocalName  
-- You can retrieve namespace URI part from the QName using the namespace-uri-from-QName() function  
SELECT xmlCol.query('declare default element namespace "QNameXSD"; namespace-uri-from-QName(/root[1])')  
FROM T  
-- Result = https://someURI  
```  
  
## <a name="see-also"></a>另請參閱  
 [QNames &#40;XQuery&#41;的相關函數 ](./functions-related-to-qnames-expanded-qname.md)  
  
