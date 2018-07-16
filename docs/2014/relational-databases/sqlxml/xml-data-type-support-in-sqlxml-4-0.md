---
title: xml 資料類型支援在 SQLXML 4.0 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLXML, xml data type support
- xml data type [SQL Server], SQLXML
ms.assetid: 9a6f5ad8-4a8f-4de7-ac17-81d5ccf78459
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 639dbfab6191b7266c367997396fa0d127031e5c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37296358"
---
# <a name="xml-data-type-support-in-sqlxml-40"></a>xml 資料類型在 SQLXML 4.0 中的支援
  開頭[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支援 XML 輸入資料使用`xml`資料型別。 本主題提供有關 SQLXML 4.0 如何識別 `xml` 資料類型之執行個體與實作其支援的資訊。  
  
## <a name="working-with-xml-data-types"></a>使用 xml 資料類型  
 為了解如何使用實作 `xml` 資料類型資料行之 SQL 資料表的詳細資訊，提供下列範例：  
  
|工作|範例|主題|  
|----------|-------------|-----------|  
|如何在 XML 檢視中對應與包含 `xml` 資料行|「將 XML 元素對應至 XML 資料類型資料行」|[XSD 元素和屬性對資料表和資料行的預設對應&#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)|  
|如何使用 Updategrams 將資料插入 `xml` 資料行|「將資料插入至 XML 資料類型資料行」|[使用 XML Updategram 插入資料&#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)|  
|將 XML 資料大量載入到 `xml` 資料行中|「大量載入到 xml 資料類型資料行」|[XML 大量載入範例&#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)|  
  
## <a name="guidelines-and-limitations"></a>指導方針與限制  
  
-   **\<xsd： 任何 >** 無法對應至資料行，包括`xml`資料型別。 在 SQLXML 中針對此案例的支援會透過 `sql:overflow-field` 註解提供。 另一個因應措施為，對應 `xml` 資料類型欄位做為 `xsd:anyType` 的元素。 此因應措施會在上述資料表中參考之「將 XML 元素對應至 XML 資料類型資料行」範例中示範。  
  
-   不支援 `xml` 資料類型資料行內容中的 XPath 查詢。  
  
-   在不支援 (例如 `xml` 和 `sql:relationship`) 或允許的註解中使用 `sql:key-fields` 資料類型資料行將會導致 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤，實作 SQLXML 4.0 的中間層元件將不會捕捉到這個錯誤。 發生這個錯誤是因為 SQLXML 不需要 SQL 類型資訊。 這類似於其他資料類型的 SQLXML 行為，例如 BLOB 和二進位類型。  
  
-   只有 XSD 結構描述支援對應 `xml` 資料行。 XDR 結構描述不支援對應 `xml` 資料行。  
  
-   SQLXML 4.0 會依賴 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中提供的 XML 剖析支援。 `xml` 資料行可以當做具類型的 XML 或不具類型的 XML 進行對應。 在任一種情況下，SQLXML 4.0 都不會驗證輸入 XML。  如果輸入 XML 無效或格式不正確，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將其回報給 SQLXML，並將使用者傳回的任何相關錯誤資訊傳播給使用者。  
  
-   SQLXML 4.0 會依賴 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中提供的 DTD 有限支援。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允許在 `xml` 資料類型資料中使用內部 DTD，這可用於提供預設值，並將實體參考取代為其展開的內容。 SQLXML 會將 XML 資料以「現況」傳遞 (包括內部 DTD) 到伺服器。 您可以使用協力廠商工具將 DTD 轉換成 XML 結構描述 (XSD) 文件，並將包含內嵌 XML 結構描述的資料載入到資料庫中。  
  
-   SQLXML 4.0 不會保留 XML 宣告處理指示 （例如） 為基礎的行為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 但是，系統會將 XML 宣告視為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] XML 剖析器的指示詞，而且在資料轉換為 `xml` 資料類型之後，會遺失其屬性 (version、encoding 和 standalone)。 XML 資料會當做 UCS-2 儲存在內部。 系統會保留 XML 執行個體中的其他所有處理指示；這些指示可用於 `xml` 資料行，而且可由 SQLXML 支援。  
  
## <a name="see-also"></a>另請參閱  
 [XML 資料 &#40;SQL Server&#41;](../xml/xml-data-sql-server.md)  
  
  
