---
title: WITH XMLNAMESPACES (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WITH_XMLNAMESPACES_TSQL
- WITH XMLNAMESPACES
dev_langs:
- TSQL
helpviewer_keywords:
- adding XML namespaces
- XML namespace declarations [SQL Server]
- clauses [SQL Server], WITH XMLNAMESPACES
- WITH XMLNAMESPACES clause
- declaring XML namespaces
ms.assetid: 3b32662b-566f-454d-b7ca-e247002a9a0b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 12af8c813fd61b4f4c9040d72e19173ef810e80f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "76909788"
---
# <a name="with-xmlnamespaces"></a>WITH XMLNAMESPACES
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  宣告一或多個 XML 命名空間。  
  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
WITH XMLNAMESPACES ( <XML namespace declaration item>  
[ { , <XML namespace declaration item> }...] )   
  
<XML namespace declaration item> ::=  
<xml_namespace_uri> AS <xml_namespace_prefix>  
| <XML default namespace declaration item>  
<xml_namespace_uri> ::= <character string literal>  
```  
  
```  
  
<xml_namespace_prefix> ::= <identifier>  
```  
  
```  
  
<XML default namespace declaration item> ::=  
DEFAULT <xml_namespace_uri>  
  
```  
  
## <a name="arguments"></a>引數  
 *xml_namespace_uri*  
 識別所宣告之 XML 命名空間的統一資源識別碼 (URI)。 *xml_namespace_uri* 是 SQL 字串。  
  
 *xml_namespace_prefix*  
 指定要對應並且與 *xml_namespace_uri* 中指定的命名空間 URI 值相關聯的前置詞。 *xml_namespace_prefix* 必須是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別碼。  
  
## <a name="remarks"></a>備註  
 在另外還包含一般資料表運算式的陳述式中使用 WITH XMLNAMESPACES 子句時，陳述式中的 WITH XMLNAMESPACES 子句必須位在一般資料表運算式之前。  
  
 當您使用 WITH XMLNAMESPACES 子句時，下列一般語法規則適用：  
  
-   每一個 XML 命名空間宣告必須包含至少一個 XML 預設命名空間宣告項目。  
  
-   使用的每一個 XML 命名空間前置詞必須是非移植 (non-colonized) 名稱 (NCName)，其中冒號字元 (:) 不是名稱的一部分。  
  
-   您不能定義兩次命名空間前置詞。  
  
-   XML 命名空間前置詞和 URI 有區分大小寫。  
  
-   無法宣告 XML 命名空間前置詞 `xmlns`。  
  
-   XML 命名空間前置詞 `xml` 不能以命名空間 URI `'http://www.w3.org/XML/1998/namespace'` 以外的命名空間覆寫，而且這個 URI 不能被指派不同的前置詞。  
  
-   當 ELEMENTS XSINIL 指示詞使用於查詢時，不能重新宣告 XML 命名空間前置詞 `xsi`。  

-   不需要宣告 'http://www.w3.org/2001/XMLSchema-instance '，即可使用 xsi 標準命名空間。 如果未指定，XML/XPATH 處理器會隱含地予以新增，且只要在 XML 文件中正確宣告 'http://www.w3.org/2001/XMLSchema-instance ' 結構描述，xpath 運算式就能使用 xsi 前置詞。

-   URI 字串值是根據目前資料庫定序字碼頁來編碼，在內部是轉換成 Unicode。  
  
-   XML 命名空間 URI 是遵照用於 **xs:anyURI** 的 XSD 空白摺疊規則而摺疊的空白。 另外，請注意，在 XML 命名空間 URI 值上不執行 entitization 或 deentitization。  

-   將檢查 XML 命名空間 URI 是否有無效的 XML 1.0 字元，如果有找到 (例如，U+0007)，就會引發錯誤。  
  
-   XML 命名空間 URI (在摺疊所有空白之後) 不得為長度零的字串，否則會發生「無效空白命名空間 URI」錯誤。  
  
-   在 WITH 子句的內容中已保留 XMLNAMESPACES 關鍵字。  
  
## <a name="examples"></a>範例  
 如需範例，請參閱[使用 WITH XMLNAMESPACES 將命名空間加入至查詢](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)。  
  
## <a name="see-also"></a>另請參閱  
 [XQuery 語言參考 &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)  
  
  
