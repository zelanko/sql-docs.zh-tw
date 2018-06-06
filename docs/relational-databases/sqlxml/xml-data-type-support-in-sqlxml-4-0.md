---
title: xml 資料類型支援在 SQLXML 4.0 |Microsoft 文件
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
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
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 68cb00ced8f77b5921be07a3f6383d4436f0bade
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="xml-data-type-support-in-sqlxml-40"></a>xml 資料類型在 SQLXML 4.0 中的支援
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  開頭為[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支援 XML 輸入資料使用**xml**資料型別。 本主題提供有關 SQLXML 4.0 如何識別的執行個體的資訊**xml**資料型別，而且會實作其支援的。  
  
## <a name="working-with-xml-data-types"></a>使用 xml 資料類型  
 若要了解更多有關如何使用可實作 SQL 資料表**xml**資料類型資料行，提供下列的範例：  
  
|工作|範例|主題|  
|----------|-------------|-----------|  
|如何對應與包含**xml** XML 檢視中的資料行|「將 XML 元素對應至 XML 資料類型資料行」|[XSD 元素和屬性對資料表和資料行的預設對應&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)|  
|如何將資料插入至**xml** updategram 的資料行|「將資料插入至 XML 資料類型資料行」|[使用 XML Updategram 插入資料&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)|  
|大量載入 XML 資料轉換成**xml**資料行|「大量載入到 xml 資料類型資料行」|[XML 大量載入範例 & #40;SQLXML 4.0 & #41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)|  
  
## <a name="guidelines-and-limitations"></a>指導方針與限制  
  
-   **\<xsd： 任何 >** 無法對應至資料行，包括**xml**資料型別。 這種情況下透過提供的 SQLXML 中支援**sql: overflow-field-欄位**註解。 另一個解決方法是將對應**xml**做為項目資料類型欄位**具有 xsd: anytype**。 此因應措施會在上述資料表中參考之「將 XML 元素對應至 XML 資料類型資料行」範例中示範。  
  
-   XPath 查詢的內容**xml**不支援資料類型資料行。  
  
-   使用**xml**註釋不支援中的資料類型資料行 (例如**sql: relationship**和**sql: key-fields-欄位**) 或允許將會造成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不會捕捉到的中介層元件，可實作 SQLXML 4.0 中的錯誤。 發生這個錯誤是因為 SQLXML 不需要 SQL 類型資訊。 這類似於其他資料類型的 SQLXML 行為，例如 BLOB 和二進位類型。  
  
-   對應**xml**只針對 XSD 結構描述支援的資料行。 XDR 結構描述不支援對應**xml**資料行。  
  
-   SQLXML 4.0 會依賴 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中提供的 XML 剖析支援。 **Xml**資料行可以是對應為具類型的 XML 或不具類型的 XML。 在任一種情況下，SQLXML 4.0 都不會驗證輸入 XML。  如果輸入 XML 無效或格式不正確，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將其回報給 SQLXML，並將使用者傳回的任何相關錯誤資訊傳播給使用者。  
  
-   SQLXML 4.0 會依賴 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中提供的 DTD 有限支援。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允許內部 DTD 中**xml**資料類型的資料，可以用來提供預設值，以及實體參考取代為其展開的內容。 SQLXML 會將 XML 資料以「現況」傳遞 (包括內部 DTD) 到伺服器。 您可以使用協力廠商工具將 DTD 轉換成 XML 結構描述 (XSD) 文件，並將包含內嵌 XML 結構描述的資料載入到資料庫中。  
  
-   SQLXML 4.0 不會保留 XML 宣告處理指示 （例如） 為基礎的行為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 相反地，XML 宣告視為指示詞[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]XML 剖析器和它的屬性 （版本、 編碼和獨立） 之後會遺失資料轉換成**xml**資料型別。 XML 資料會當做 UCS-2 儲存在內部。 會保留 XML 執行個體中的所有其他處理指示。中，則允許**xml**資料行和可由 SQLXML 支援。  
  
## <a name="see-also"></a>另請參閱  
 [XML 資料 &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
