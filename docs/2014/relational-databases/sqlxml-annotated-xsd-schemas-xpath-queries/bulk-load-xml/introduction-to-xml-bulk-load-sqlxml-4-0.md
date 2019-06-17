---
title: XML 大量載入 (SQLXML 4.0) 簡介 |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- nontransacted XML Bulk Load operations
- XML Bulk Load [SQLXML], about XML Bulk Load
- bulk load [SQLXML], about bulk load
- transacted XML Bulk Load operations
- streaming XML data
ms.assetid: 38bd3cbd-65ef-4c23-9ef3-e70ecf6bb88a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d257b6eee1fb3adc0ba611f58a1d5eea5adf3f86
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013385"
---
# <a name="introduction-to-xml-bulk-load-sqlxml-40"></a>XML 大量載入簡介 (SQLXML 4.0)
  XML 大量載入是獨立的 COM 物件，可讓您將半結構化的 XML 資料載入至 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料表。  
  
 您可以使用 INSERT 陳述式和 OPENXML 函數將 XML 資料插入至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫，不過當您需要插入大量的 XML 資料時，大量載入公用程式可以提供較佳的效能。  
  
 XML 大量載入物件模型的 Execute 方法會採用兩個參數：  
  
-   註解 XML 結構描述定義 (XSD) 或 XML 資料精簡 (XDR) 結構描述。 XML 大量載入公用程式在識別其中將插入 XML 資料的 SQL Server 資料表時，會解譯此對應結構描述以及結構描述中所指定的註解。  
  
-   XML 文件或文件片段 (文件片段是沒有單一最上層元素的文件)。 可以指定 XML 大量載入能從中讀取的檔案名稱或資料流。  
  
 XML 大量載入會解譯對應結構描述並識別其中將插入 XML 資料的資料表。  
  
 這裡假設您熟悉下列的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 功能：  
  
-   註解 XSD 和 XDR 結構描述。 如需有關註解式 XSD 結構描述的詳細資訊，請參閱 <<c0> [ 註解式 XSD 結構描述簡介&#40;SQLXML 4.0&#41;](../../sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)。</c0> 註解式 XDR 結構描述的相關資訊，請參閱[註解式 XDR 結構描述&#40;在 SQLXML 4.0 中已被取代&#41;](../../sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 大量插入機制，例如 [!INCLUDE[tsql](../../../includes/tsql-md.md)] BULK INSERT 陳述式和 bcp 公用程式。 如需詳細資訊，請參閱 < [BULK INSERT &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/bulk-insert-transact-sql)並[bcp 公用程式](../../../tools/bcp-utility.md)。  
  
## <a name="streaming-of-xml-data"></a>XML 資料的資料流  
 因為來源 XML 文件可能很大，所以不會將整個文件讀入記憶體來進行大量載入處理， 而是由 XML 大量載入以資料流的方式解譯 XML 資料，再加以讀取。 此公用程式讀取資料時會識別資料庫資料表，從 XML 資料來源產生適當的記錄，然後再將記錄傳送到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 進行插入。  
  
 例如，下列的來源 XML 文件所組成 **\<客戶 >** 項目並 **\<順序 >** 子項目：  
  
```  
<Customer ...>  
    <Order.../>  
    <Order .../>  
     ...  
</Customer>  
...  
```  
  
 XML 大量載入讀取 **\<客戶 >** 項目，為 Customertable 產生一筆記錄。 當讀取 **\</Customer >** 結束標記時，XML 大量載入將該記錄插入資料表中插入[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 在同一個方法，當它讀取 **\<順序 >** 元素，XML 大量載入 Ordertable，產生一筆記錄，然後將插入到該記錄[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料表，在讀取時 **\</ 排序 >** 結束標記。  
  
## <a name="transacted-and-nontransacted-xml-bulk-load-operations"></a>交易和非交易 XML 大量載入作業  
 XML 大量載入可以在交易或非交易模式中操作。 通常效能會最佳化如果您是以非交易模式的大量載入： 也就是 [交易] 屬性設定為 FALSE) 和其中一個下列條件成立：  
  
-   其中要大量載入資料的資料表是空的，且沒有任何索引。  
  
-   資料表具有資料和唯一的索引。  
  
 非交易的方法並不保證能在大量載入程序發生問題時進行回復 (雖然可能可以進行部分回復)。 當資料表是空白時，適用非交易的大量載入。 因此在發生問題時，您可以清除資料庫，然後再次啟動 XML 大量載入。  
  
> [!NOTE]  
>  在非交易模式中，XML 大量載入會使用預設的內部交易並加以認可。 當交易屬性設定為 TRUE 時，XML 大量載入不會呼叫認可此交易。  
  
 如果交易屬性設定為 TRUE，XML 大量載入會建立暫存檔案，在對應結構描述中所識別的每個資料表各一個。 XML 大量載入會先把來自來源 XML 文件的記錄儲存在這些暫存檔中。 接著 [!INCLUDE[tsql](../../../includes/tsql-md.md)] BULK INSERT 陳述式會從檔案擷取這些記錄，然後將它們儲存在對應的資料表中。 您可以使用 TempFilePath 屬性來指定這些暫存檔的位置。 您必須確定用於 XML 大量載入的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 帳戶具有這個路徑的存取權。 如果未指定 TempFilePath 內容，TEMP 環境變數中指定的預設檔案路徑用來建立暫存檔案。  
  
 如果為 FALSE （預設值） 設定交易屬性，XML 大量載入會使用 IRowsetFastLoad 來大量載入資料的 OLE DB 介面。  
  
 如果 ConnectionString 屬性設定的連接字串，而且交易屬性設定為 TRUE，XML 大量載入會在它自己的交易內容中運作。 (例如，XML 大量載入會啟動本身的交易，然後依需要進行認可或回復)。  
  
 如果 ConnectionCommand 屬性設定的連線，使用現有的連接物件和交易屬性設定為 TRUE，XML 大量載入不會分別發出 COMMIT 或 ROLLBACK 陳述式在成功或失敗。 如果發生錯誤，XML 大量載入會傳回適當的錯誤訊息。 至於是否要發出 COMMIT 或 ROLLBACK 陳述式，則會留給起始大量載入的用戶端決定。 使用於 XML 大量載入的連接物件應該是類型 ICommand 的或者是 ADO 命令物件。  
  
 在 SQLXML 4.0 中，ConnectionObject 無法搭配交易屬性設定為 FALSE。 因為無法為傳入的工作階段上開啟一個以上的 IRowsetFastLoad 介面 ConnectionObject 不被支援的非交易模式。  
  
  
