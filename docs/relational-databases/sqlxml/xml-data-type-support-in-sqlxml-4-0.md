---
title: xml 資料類型在 SQLXML 4.0 中的支援
description: 瞭解 SQLXML 4.0 如何辨識 xml 資料類型的實例，並為其執行支援。
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, xml data type support
- xml data type [SQL Server], SQLXML
ms.assetid: 9a6f5ad8-4a8f-4de7-ac17-81d5ccf78459
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0c2400239b5ad8d19733b1fa74f7750c6edc4382
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479179"
---
# <a name="xml-data-type-support-in-sqlxml-40"></a>xml 資料類型在 SQLXML 4.0 中的支援
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  從開始 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 **xml** 資料類型支援 xml 具類型的資料。 本主題提供 SQLXML 4.0 如何辨識 **xml** 資料類型的實例，並為其提供支援的相關資訊。  
  
## <a name="working-with-xml-data-types"></a>使用 xml 資料類型  
 若要深入瞭解如何使用可執行 **xml** 資料類型資料行的 SQL 資料表，請提供下列範例：  
  
|Task|範例|主題|  
|----------|-------------|-----------|  
|如何在 XML 視圖中對應和包含 **xml** 資料行|「將 XML 元素對應至 XML 資料類型資料行」|[XSD 元素和屬性與資料表和資料行的預設對應 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)|  
|如何使用 updategram 將資料插入至 **xml** 資料行|「將資料插入至 XML 資料類型資料行」|[使用 XML Updategram 插入資料 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)|  
|將 XML 資料大量載入至 **xml** 資料行|「大量載入到 xml 資料類型資料行」|[XML 大量載入範例 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)|  
  
## <a name="guidelines-and-limitations"></a>指導方針與限制  
  
-   **\<xsd:any>** 無法對應至包含 **xml** 資料類型的資料行。 此案例的 SQLXML 支援是透過 **sql：溢位欄位** 批註提供。 另一個解決方法是將 **xml** 資料類型欄位對應為 **xsd： anyType** 的元素。 此因應措施會在上述資料表中參考之「將 XML 元素對應至 XML 資料類型資料行」範例中示範。  
  
-   不支援將 XPath 查詢至 **xml** 資料類型資料行的內容。  
  
-   在不支援的注釋中使用 **xml** 資料類型資料行 (例如 **sql： relationship** 和 **sql：索引鍵-欄位**) 或允許的，將會導致 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行 SQLXML 4.0 的中介層元件未攔截到的錯誤。 發生這個錯誤是因為 SQLXML 不需要 SQL 類型資訊。 這類似於其他資料類型的 SQLXML 行為，例如 BLOB 和二進位類型。  
  
-   只有 XSD 架構支援對應 **xml** 資料行。 XDR 架構不支援對應 **xml** 資料行。  
  
-   SQLXML 4.0 會依賴 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中提供的 XML 剖析支援。 **Xml** 資料行可以對應為具類型的 xml 或不具類型的 xml。 在任一種情況下，SQLXML 4.0 都不會驗證輸入 XML。  如果輸入 XML 無效或格式不正確，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將其回報給 SQLXML，並將使用者傳回的任何相關錯誤資訊傳播給使用者。  
  
-   SQLXML 4.0 會依賴 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中提供的 DTD 有限支援。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允許 **xml** 資料類型資料中的內部 DTD，可用來提供預設值，並將實體參考取代為其展開的內容。 SQLXML 會將 XML 資料以「現況」傳遞 (包括內部 DTD) 到伺服器。 您可以使用協力廠商工具將 DTD 轉換成 XML 結構描述 (XSD) 文件，並將包含內嵌 XML 結構描述的資料載入到資料庫中。  
  
-   SQLXML 4.0 不會保留 XML 宣告處理指示 (例如，根據的行為 ) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 相反地，XML 宣告會被視為 xml 剖析器的指示詞 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，而其屬性 (版本、編碼和獨立) 在資料轉換成 **xml** 資料類型後就會遺失。 XML 資料會當做 UCS-2 儲存在內部。 XML 實例中的所有其他處理指示都會保留;它們在 **xml** 資料行中是允許的，而且可由 SQLXML 支援。  
  
## <a name="see-also"></a>另請參閱  
 [XML 資料 &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
