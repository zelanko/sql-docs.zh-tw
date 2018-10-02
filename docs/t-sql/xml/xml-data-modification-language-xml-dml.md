---
title: XML 資料修改語言 (XML DML) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- modifying data [SQL Server], XML DML
- XML [SQL Server], DML
- XML DML [SQL Server]
- data modification language [XML DML]
- data modifications [XML DML]
- DML [XML in SQL Server]
- XQuery, XML DML
- xml data type [SQL Server], XML DML
ms.assetid: 20ce50d2-c07b-4e41-93a7-1380d2cd49cb
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7a4c6c273aba15027c18d96e6d0295be2e639629
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47831877"
---
# <a name="xml-data-modification-language-xml-dml"></a>XML 資料修改語言 (XML DML)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  XML 資料修改語言 (XML DML) 是 XQuery 語言的延伸。 如 W3C 所定義的，XQuery 語言缺少「資料操作」(DML) 的部份。 本主題中所介紹的 XML DML (同時也是 XQuery 語言)，可提供功能完整的查詢及資料修改語言，讓您可以針對 **xml** 資料類型來使用。  
  
 XML DML 會將下列區分大小寫的關鍵字加入到 XQuery 中：  
  
-   **insert**  
  
-   **delete**  
  
-   **replace value of**  
  
 如 [XML 資料類型和資料行 &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-type-and-columns-sql-server.md) 中所描述的，您可以建立 **xml** 類型的變數及資料行，並將 XML 文件或片段指派給它們。 若要修改或更新這些 XML 執行個體，請執行下列動作：  
  
-   使用 **xml** 資料類型的 [modify() 方法 (xml 資料類型)](../../t-sql/xml/modify-method-xml-data-type.md)。  
  
-   在 **modify()** 方法內指定適當的 XML DML 陳述式。  
  
 請注意，有一些屬性不能被插入、刪除或修改它們的值。 例如：  
  
-   若為具類型或不具類型的 **xml**，屬性為 **xmlns**、**xmlns:\*** 和 **xml:base**。  
  
-   若只為具類型的 **xml**，則屬性為 **xsi:nil** 及 **xsi:type**。  
  
 其他限制包括下列項目：  
  
-   若為具類型或不具類型的 **xml**，則插入屬性 **xml:base** 會失敗。  
  
-   若為具類型的 **xml**，則刪除及修改 **xsi:nil** 屬性會失敗。 若為不具類型的 **xml**，您可以刪除屬性或修改其屬性值。  
  
-   若為具類型的 **xml**，則修改 **xs:type** 屬性的值會失敗。 若為不具類型的 **xml**，您可以修改屬性值。  
  
 在修改具類型的 XML 執行個體時，最後的格式必須是該類型的有效執行個體。 否則，就會傳回驗證錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [insert &#40;XML DML&#41;](../../t-sql/xml/insert-xml-dml.md)   
 [delete &#40;XML DML&#41;](../../t-sql/xml/delete-xml-dml.md)   
 [replace value of &#40;XML DML&#41;](../../t-sql/xml/replace-value-of-xml-dml.md)   
 [比較具類型的 XML 與不具類型的 XML](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [建立 XML 資料的執行個體](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 資料類型方法](../../t-sql/xml/xml-data-type-methods.md)  
  
  
