---
title: 資料列集 |Microsoft 文件
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], about rowsets
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets
- OLE DB rowsets, about rowsets
- rowsets [OLE DB]
ms.assetid: 5e7b3cbe-3670-4e18-8172-2226e0b6b142
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1d12a7c6dfc3a63d20a16a4a4361ffd46e4f8972
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="rowsets"></a>資料列集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  資料列集是一組資料列，其中包含資料的資料行。 資料列集是能讓所有 OLE DB 資料提供者公開表格形式結果集資料的核心物件。  
  
 取用者使用建立工作階段之後 **:: Createsession**方法中，取用者可以使用**IOpenRowset**或**IDBCreateCommand**上要建立資料列集的工作階段的介面。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者支援這兩種介面。 此處描述這兩種方法。  
  
-   建立資料列集呼叫**iopenrowset:: Openrowset**方法。  
  
     這相當於在單一資料表上建立資料列集。 此方法會從單一基底資料表開啟並傳回包含所有資料列的資料列集。 引數的其中一個**OpenRowset**是資料表識別碼，可識別要從中建立資料列集的資料表。  
  
-   建立命令物件，藉由呼叫**idbcreatecommand:: Createcommand**方法。  
  
     命令物件會執行提供者支援的命令。 利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者，取用者可以指定任何 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，例如 SELECT 陳述式或預存程序的呼叫。 使用命令物件建立資料列集的步驟如下：  
  
    1.  取用者可以呼叫**idbcreatecommand:: Createcommand**方法以取得命令物件上要求的工作階段上**ICommandText**命令物件上的介面。 這**ICommandText**介面設定及擷取實際的命令文字。 取用者會填入文字命令藉由呼叫**icommandtext:: Setcommandtext**方法。  
  
    2.  使用者呼叫**icommand:: Execute**命令上的方法。 命令執行時所建立的資料列集物件包含來自命令的結果集。  
  
 取用者可以使用**ICommandProperties**介面，以取得或設定所執行的命令所傳回的資料列集屬性**icommand:: Execute**介面。 最常要求的屬性為資料列集必須支援的介面。 除了介面之外，取用者可以要求修改資料列集或介面之行為的屬性。  
  
 取用者釋放資料列集與**irowset:: Release**方法。 釋放資料列集時，也會釋放取用者在該資料列集上保留的所有資料列控制代碼。 釋放資料列集不會釋放存取子。 如果您有**IAccessor**介面，它仍有釋出。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [以 IOpenRowset 建立資料列集](../../relational-databases/native-client-ole-db-rowsets/creating-a-rowset-with-iopenrowset.md)  
  
-   [使用 icommand:: Execute 建立資料列集](../../relational-databases/native-client-ole-db-rowsets/creating-rowsets-with-icommand-execute.md)  
  
-   [資料列集屬性和行為](../../relational-databases/native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)  
  
-   [資料列集和 SQL Server 資料指標](../../relational-databases/native-client-ole-db-rowsets/rowsets-and-sql-server-cursors.md)  
  
-   [提取資料列](../../relational-databases/native-client-ole-db-rowsets/fetching-rows.md)  
  
-   [擷取單一資料列使用 irow 來](../../relational-databases/native-client-ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
-   [書籤](../../relational-databases/native-client-ole-db-rowsets/bookmarks.md)  
  
-   [更新資料集中的資料列集](../../relational-databases/native-client-ole-db-rowsets/updating-data-in-rowsets.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
