---
title: 序列和 Q 名稱 （XQuery） |微軟文檔
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sequence [XQuery]
- XQuery, sequence
- QName [XQuery]
- predefined namespaces [XML in SQL Server]
ms.assetid: 3593ac26-dd78-4bf0-bb87-64fbcac5f026
author: rothja
ms.author: jroth
ms.openlocfilehash: c71a7139c3adb354923b3c953b367ab506f30545
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2020
ms.locfileid: "80380779"
---
# <a name="sequence-and-qnames-xquery"></a>順序和 QName (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  此主題描述下列 XQuery 基礎概念：  
  
-   順序  
  
-   QName 和預先定義的命名空間  
  
## <a name="sequence"></a>順序  
 在 XQuery 中，運算式的結果是由 XML 節點清單和 XSD 不可部份完成類型的執行個體所組合之序列。 序列中的個別項目 (Entry) 稱為項目 (Item)。 序列中的項目可以是下列其中一項：  
  
-   一個節點，例如元素、屬性、文字、處理指示、註解或文件。  
  
-   一個不可部份完成的值，例如 XSD 簡單類型的執行個體。  
  
 例如，下列查詢由兩個元素節點項目的序列建構而成：  
  
```  
SELECT Instructions.query('  
     <step1> Step 1 description goes here</step1>,  
     <step2> Step 2 description goes here </step2>  
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7;  
  
```  
  
 以下是結果：  
  
```  
<step1> Step 1 description goes here </step1>  
<step2> Step 2 description goes here </step2>   
```  
  
 在以上的查詢中，在 `,` 建構末端的逗號 (`<step1>`) 是序列建構函式，而且是必要的。 結果中加入的空白僅供說明使用，本文件集的所有範例結果中都會包含。  
  
 以下是其他您應知道的序列相關資訊：  
  
-   如果查詢導致時序中包含另一個時序，則被包含的時序會單層化到容器時序中。 例如，序列 ((1,2, (3,4,5)),6) 會在資料模型中單層化為 (1, 2, 3, 4, 5, 6)。  
  
    ```  
    DECLARE @x xml;  
    SET @x = '';  
    SELECT @x.query('(1,2, (3,4,5)),6');  
    ```  
  
-   空白序列是不包含任何項目的序列， 以 "()" 來表示。  
  
-   只具有一個項目的序列可以視為不可部份完成的值，反之亦然。 也就是說，(1) = 1。  
  
 在此實作中，序列必須為同質。 也就是說，您只能有不可部份完成值的序列或節點的序列其中一項。 例如，下列為有效的序列：  
  
```  
DECLARE @x xml;  
SET @x = '';  
-- Expression returns a sequence of 1 text node (singleton).  
SELECT @x.query('1');  
-- Expression returns a sequence of 2 text nodes  
SELECT @x.query('"abc", "xyz"');  
-- Expression returns a sequence of one atomic value. data() returns  
-- typed value of the node.  
SELECT @x.query('data(1)');  
-- Expression returns a sequence of one element node.   
-- In the expression XML construction is used to construct an element.  
SELECT @x.query('<x> {1+2} </x>');  
```  
  
 下列查詢會傳回錯誤，因為不支援異質序列。  
  
```  
SELECT @x.query('<x>11</x>, 22');  
```  
  
## <a name="qname"></a>QName  
 XQuery 中的每一個識別碼都是一個 QName。 QName 是由命名空間前置詞和本機名稱組成。 在此實作中，XQuery 中的變數名稱為 QName，而且不能有前置詞。  
  
 請考慮以下示例，其中針對未鍵入的**xml**變數指定查詢：  
  
```  
DECLARE @x xml;  
SET @x = '<Root><a>111</a></Root>';  
SELECT @x.query('/Root/a');  
```  
  
 在運算式 (`/Root/a`) 中，`Root` 和 `a` 是 QName。  
  
 在下面的示例中，針對鍵入的**xml**列指定了查詢。 查詢遍比較第一個工作\<中心位置的所有步驟>元素。  
  
```  
SELECT Instructions.query('  
   declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $Step in /AWMI:root/AWMI:Location[1]/AWMI:step  
      return  
           string($Step)   
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7;  
```  
  
 在查詢運算式中，請注意下列事項：  
  
-   `AWMI root`、`AWMI:Location`、`AWMI:step` 和 `$Step` 全部都是 QName。 `AWMI` 是前置詞，而 `root`、`Location` 和 `Step` 都是本機名稱。  
  
-   `$step` 變數是 QName，而且沒有前置詞。  
  
 下列命名空間已預先定義，以和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的 XQuery 支援一起使用。  
  
|前置詞|URI|  
|------------|---------|  
|xs|http://www.w3.org/2001/XMLSchema|  
|xsi|http://www.w3.org/2001/XMLSchema-instance|  
|xdt|http://www.w3.org/2004/07/xpath-datatypes|  
|fn|http://www.w3.org/2004/07/xpath-functions|  
|(無前置詞)|`urn:schemas-microsoft-com:xml-sql`|  
|sqltypes|`https://schemas.microsoft.com/sqlserver/2004/sqltypes`|  
|Xml|`http://www.w3.org/XML/1998/namespace`|  
|(無前置詞)|`https://schemas.microsoft.com/sqlserver/2004/SOAP`|  
  
 您創建的每個資料庫都有**sys** XML 架構集合。 此集合會保留這些結構描述，所以從使用者建立的任何 XML 結構描述集合都能存取這些結構描述。  
  
> [!NOTE]  
>  此實現不支援 中的`local`XQuery 規範中http://www.w3.org/2004/07/xquery-local-functions所述的首碼。  
  
## <a name="see-also"></a>另請參閱  
 [XQuery 基本概念](../xquery/xquery-basics.md)  
  
  
