---
title: XML 大量載入 (SQLXML) 簡介
description: 深入瞭解 XML 大量載入公用程式，這是 SQLXML 4.0 中的獨立 COM 物件，可讓您將半結構化 XML 資料載入 Microsoft SQL Server 資料表中。
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9bd7ea649bc00090c64b312f007b40ea15bdf9bb
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97439676"
---
# <a name="introduction-to-xml-bulk-load-sqlxml-40"></a>XML 大量載入簡介 (SQLXML 4.0) 
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  XML 大量載入是獨立的 COM 物件，可讓您將半結構化的 XML 資料載入至 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料表。  
  
 您可以使用 INSERT 陳述式和 OPENXML 函數將 XML 資料插入至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫，不過當您需要插入大量的 XML 資料時，大量載入公用程式可以提供較佳的效能。  
  
 XML 大量載入物件模型的 Execute 方法會採用兩個參數：  
  
-   註解 XML 結構描述定義 (XSD) 或 XML 資料精簡 (XDR) 結構描述。 XML 大量載入公用程式在識別其中將插入 XML 資料的 SQL Server 資料表時，會解譯此對應結構描述以及結構描述中所指定的註解。  
  
-   XML 文件或文件片段 (文件片段是沒有單一最上層元素的文件)。 可以指定 XML 大量載入能從中讀取的檔案名稱或資料流。  
  
 XML 大量載入會解譯對應結構描述並識別其中將插入 XML 資料的資料表。  
  
 這裡假設您熟悉下列的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 功能：  
  
-   註解 XSD 和 XDR 結構描述。 如需批註式 XSD 架構的詳細資訊，請參閱 [批註式 Xsd 架構簡介 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)。 如需批註式 XDR 架構的詳細資訊，請參閱 [SQLXML 4.0&#41;中 &#40;取代的批註式 Xdr 架構 ](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 大量插入機制，例如 [!INCLUDE[tsql](../../../includes/tsql-md.md)] BULK INSERT 陳述式和 bcp 公用程式。 如需詳細資訊，請參閱 [BULK INSERT &#40;transact-sql&#41;](../../../t-sql/statements/bulk-insert-transact-sql.md) 和 [bcp 公用程式](../../../tools/bcp-utility.md)。  
  
## <a name="streaming-of-xml-data"></a>XML 資料的資料流  
 因為來源 XML 文件可能很大，所以不會將整個文件讀入記憶體來進行大量載入處理， 而是由 XML 大量載入以資料流的方式解譯 XML 資料，再加以讀取。 此公用程式讀取資料時會識別資料庫資料表，從 XML 資料來源產生適當的記錄，然後再將記錄傳送到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 進行插入。  
  
 例如，下列來源 XML 檔是由 **\<Customer>** 元素和 **\<Order>** 子項目所組成：  
  
```  
<Customer ...>  
    <Order.../>  
    <Order .../>  
     ...  
</Customer>  
...  
```  
  
 當 XML 大量載入讀取 **\<Customer>** 元素時，它會產生 Customertable 的記錄。 當它讀取 **\</Customer>** 結束標記時，XML 大量載入會將該記錄插入中的資料表 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 以同樣的方式，當它讀取專案時 **\<Order>** ，XML 大量載入會產生 Ordertable 的記錄，然後在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 讀取結束標記時將該記錄插入資料表中 **\</Order>** 。  
  
## <a name="transacted-and-nontransacted-xml-bulk-load-operations"></a>交易和非交易 XML 大量載入作業  
 XML 大量載入可以在交易或非交易模式中操作。 如果您是以非交易模式大量載入，效能通常是最佳的：也就是說，Transaction 屬性會設定為 FALSE) 而且下列任一條件成立：  
  
-   其中要大量載入資料的資料表是空的，且沒有任何索引。  
  
-   資料表具有資料和唯一的索引。  
  
 非交易的方法並不保證能在大量載入程序發生問題時進行回復 (雖然可能可以進行部分回復)。 當資料表是空白時，適用非交易的大量載入。 因此在發生問題時，您可以清除資料庫，然後再次啟動 XML 大量載入。  
  
> [!NOTE]  
>  在非交易模式中，XML 大量載入會使用預設的內部交易並加以認可。 當 Transaction 屬性設定為 TRUE 時，XML 大量載入不會對此交易呼叫 commit。  
  
 如果 Transaction 屬性設定為 TRUE，則 XML 大量載入會建立暫存檔案，並針對對應架構中所識別的每個資料表建立一個檔案。 XML 大量載入會先把來自來源 XML 文件的記錄儲存在這些暫存檔中。 接著 [!INCLUDE[tsql](../../../includes/tsql-md.md)] BULK INSERT 陳述式會從檔案擷取這些記錄，然後將它們儲存在對應的資料表中。 您可以使用 TempFilePath 屬性來指定這些暫存檔案的位置。 您必須確定用於 XML 大量載入的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 帳戶具有這個路徑的存取權。 如果未指定 TempFilePath 屬性，則會使用 TEMP 環境變數中指定的預設檔案路徑來建立暫存檔案。  
  
 如果 Transaction 屬性設為 FALSE (預設設定) ，XML 大量載入會使用 OLE DB 介面 IRowsetFastLoad 來大量載入資料。  
  
 如果 ConnectionString 屬性設定連接字串，而且 Transaction 屬性設定為 TRUE，則 XML 大量載入會在它自己的交易內容中運作。 (例如，XML 大量載入會啟動本身的交易，然後依需要進行認可或回復)。  
  
 如果 ConnectionCommand 屬性設定與現有連線物件的連接，而且 Transaction 屬性設定為 TRUE，則 XML 大量載入不會在成功或失敗的情況下，分別發出 COMMIT 或 ROLLBACK 語句。 如果發生錯誤，XML 大量載入會傳回適當的錯誤訊息。 至於是否要發出 COMMIT 或 ROLLBACK 陳述式，則會留給起始大量載入的用戶端決定。 用於 XML 大量載入的連線物件應該是 ICommand 類型，或是 ADO 命令物件。  
  
 在 SQLXML 4.0 中，ConnectionObject 不能用來將 Transaction 屬性設為 FALSE。 ConnectionObject 不支援非交易模式，因為無法在傳入的會話上開啟一個以上的 IRowsetFastLoad 介面。  
  
  
