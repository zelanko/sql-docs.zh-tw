---
title: 指導方針和限制的 XML Updategram (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- updategrams [SQLXML], about updategrams
ms.assetid: b5231859-14e2-4276-bc17-db2817b6f235
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9dda62acddf1dbda2fe37c4ed458c37f5725ffdd
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "38031426"
---
# <a name="guidelines-and-limitations-of-xml-updategrams-sqlxml-40"></a>XML Updategram 的指導方針和限制 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  使用 XML Updategram 時，請記住下列事項：  
  
-   如果您要將 updategram 用於只有單一組的插入作業**\<之前 >** 並**\<之後 >** 區塊**\<之前>** 區塊，則可以省略。 相反地，如果刪除作業， **\<之後 >** 區塊，則可以省略。  
  
-   如果您要使用 updategram 與多個**\<之前 >** 並**\<之後 >** 區塊，以**\<同步 >** 標記，兩者**\<之前 >** 區塊並**\<之後 >** 表單必須指定區塊**\<之前 >** 和**\<之後 >** 組。  
  
-   Updategram 中的更新會套用到 XML 結構描述所提供的 XML 檢視。 因此，若要讓預設的對應成功，您必須在 Updategram 中指定結構描述檔案名稱，或者，如果沒有提供檔案名稱，元素和屬性名稱必須符合資料庫中的資料表和資料行名稱。  
  
-   SQLXML 4.0 要求 Updategram 中的所有資料行值都必須在提供的結構描述 (XDR 或 XSD) 中明確對應，才能構成其子元素的 XML 檢視。 此行為不同於舊版的 SQLXML，允許未對應的結構描述中，如果這意味著一部分的外部索引鍵資料行的值**sql: relationship**註釋。 (請注意，此變更不會影響主索引鍵值傳播到子元素，如果沒有針對子元素明確指定任何值，仍然會發生在 SQLXML 4.0 上。  
  
-   如果您使用 updategram 來修改二進位資料行中的資料 (例如[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**映像**資料類型)，您必須提供對應結構描述，其中[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料類型 (例如**sql: datatype ="image"**) 和 XML 資料類型 (例如**dt: type ="binhex"** 或是**dt: type ="binbase64**) 必須指定。 二進位資料行的資料必須指定在 updategram 中;**sql: url-encode-編碼**updategram 會忽略在對應結構描述中指定的註解。  
  
-   當您在撰寫 XSD 結構描述，如果您指定的值**sql: relation**或是**sql: field**註解包含特殊字元，如空白字元 （例如，在"Order Details"資料表名稱），這個值必須加上方括號 （例如，"[Order Details]"）。  
  
-   使用 Updategram 時，不支援鏈結關聯性。 例如，如果資料表 A 和 C 透過使用資料表 B 的鏈結關聯性相關聯，嘗試執行 Updategram 時，會發生下列錯誤：  
  
    ```  
    There is an inconsistency in the schema provided.  
    ```  
  
     即使結構描述和 Updategram 都正確而且格式有效，如果存在鏈結關聯性，則會發生此錯誤。  
  
-   Updategram 不允許的傳遞**映像**類型做為參數的資料，在更新期間。  
  
-   二進位大型物件 (BLOB) 類型如同**text/ntext**中應不到映像**\<之前 >** 區塊時使用 updategram，因為這會將它們包含用於並行存取控制。 這可能會因為 BLOB 類型的比較限制而造成 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的問題。 比方說，LIKE 關鍵字用於 WHERE 子句中的資料行之間的比較**文字**資料類型; 不過，比較將會失敗如果資料的大小大於 8k 的 BLOB 類型。  
  
-   中的特殊字元**ntext**資料進行因為 BLOB 類型的比較限制，可能會造成某些搭配 SQLXML 4.0 的問題。 例如，"[Serializable]"中的使用**\<之前 >** updategram 時並行檢查的資料行中所使用的區塊**ntext**類型將會失敗並下列 SQLOLEDB錯誤描述：  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [Updategram 安全性考量&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
