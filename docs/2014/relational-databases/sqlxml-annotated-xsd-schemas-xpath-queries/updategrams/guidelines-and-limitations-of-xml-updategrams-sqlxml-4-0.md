---
title: XML Updategram 的指導方針和限制（SQLXML 4.0） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- updategrams [SQLXML], about updategrams
ms.assetid: b5231859-14e2-4276-bc17-db2817b6f235
author: rothja
ms.author: jroth
ms.openlocfilehash: 2e28f4258aef27403c107158dd13efe5ada02c03
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "84996235"
---
# <a name="guidelines-and-limitations-of-xml-updategrams-sqlxml-40"></a>XML Updategram 的指導方針和限制 (SQLXML 4.0)
  使用 XML Updategram 時，請記住下列事項：  
  
-   如果您針對僅具有一組和區塊的插入作業使用 updategram **\<before>** **\<after>** ，則 **\<before>** 可以省略區塊。 相反地，在刪除作業時， **\<after>** 可以省略區塊。  
  
-   如果您在標記中使用具有多個 **\<before>** 和區塊的 updategram，則 **\<after>** **\<sync>** **\<before>** 必須同時 **\<after>** 指定區塊和區塊來形成 **\<before>** 和 **\<after>** 配對。  
  
-   Updategram 中的更新會套用到 XML 結構描述所提供的 XML 檢視。 因此，若要讓預設的對應成功，您必須在 Updategram 中指定結構描述檔案名稱，或者，如果沒有提供檔案名稱，元素和屬性名稱必須符合資料庫中的資料表和資料行名稱。  
  
-   SQLXML 4.0 要求 Updategram 中的所有資料行值都必須在提供的結構描述 (XDR 或 XSD) 中明確對應，才能構成其子元素的 XML 檢視。 此行為與舊版 SQLXML 不同，如果這意味著 `sql:relationship` 註解中外部索引鍵的一部分，則允許在結構描述中不對應資料行的值  (請注意，此變更不會影響主索引鍵值傳播到子元素，如果沒有針對子元素明確指定任何值，仍然會發生在 SQLXML 4.0 上。  
  
-   如果您使用 updategram 來修改二進位資料行中的資料（例如 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] `image` 資料類型），您必須提供對應架構，其中 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 必須指定資料類型（例如， `sql:datatype="image"` ）和 XML 資料類型（例如， `dt:type="binhex"` 或 `dt:type="binbase64` ）。 二進位資料行的資料必須在 Updategram 中指定；Updategram 會忽略在對應結構描述中指定的 `sql:url-encode` 註解。  
  
-   當您要撰寫 XSD 結構描述時，如果您針對 `sql:relation` 或 `sql:field` 註解指定的值包含特殊字元，如空白字元 (例如，在 "Order Details" 資料表名稱中)，則必須以方括號括住這個值 (例如，"[Order Details]")。  
  
-   使用 Updategram 時，不支援鏈結關聯性。 例如，如果資料表 A 和 C 透過使用資料表 B 的鏈結關聯性相關聯，嘗試執行 Updategram 時，會發生下列錯誤：  
  
    ```  
    There is an inconsistency in the schema provided.  
    ```  
  
     即使結構描述和 Updategram 都正確而且格式有效，如果存在鏈結關聯性，則會發生此錯誤。  
  
-   在更新期間，Updategram 不允許將 `image` 類型資料當做參數傳遞。  
  
-   使用 updategram 時，不應該在中的區塊中使用二進位大型物件（BLOB）類型（例如 `text/ntext` 和影像） **\<before>** ，因為這會包含它們以用於並行控制。 這可能會因為 BLOB 類型的比較限制而造成 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的問題。 例如，WHERE 子句中的 LIKE 關鍵字用於 `text` 資料類型之資料行間的比較，不過，如果 BLOB 類型中，資料大小大於 8K，則比較將會失敗。  
  
-   `ntext` 資料中的特殊字元可能會因為 BLOB 類型的比較限制而造成 SQLXML 4.0 的問題。 例如，在類型資料行的並行檢查中使用 "[Serializable]" 時，在 updategram 的區塊中使用 "[Serializable]" **\<before>** `ntext` 將會失敗，並出現下列 SQLOLEDB 錯誤描述：  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [&#40;SQLXML 4.0&#41;的 Updategram 安全性考慮](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
