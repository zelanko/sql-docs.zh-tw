---
title: 資料列集 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], about rowsets
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets
- OLE DB rowsets, about rowsets
- rowsets [OLE DB]
ms.assetid: 5e7b3cbe-3670-4e18-8172-2226e0b6b142
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6eee795eb26af6f0df4bad70cc021c2fbc682bce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103575"
---
# <a name="rowsets"></a>資料列集
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  資料列集是一組資料列，其中包含資料的資料行。 資料列集是能讓所有 OLE DB 資料提供者公開表格形式結果集資料的核心物件。  
  
 取用者使用 **IDBCreateSession::CreateSession** 方法建立工作階段之後，就可以使用工作階段上的 **IOpenRowset** 或 **IDBCreateCommand** 介面建立資料列集。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者支援這兩種介面。 此處描述這兩種方法。  
  
-   呼叫 **IOpenRowset::OpenRowset** 方法來建立資料列集。  
  
     這相當於在單一資料表上建立資料列集。 此方法會從單一基底資料表開啟並傳回包含所有資料列的資料列集。 其中的 **OpenRowset** 引數是資料表識別碼，可識別要從中建立資料列集的資料表。  
  
-   呼叫 **IDBCreateCommand::CreateCommand** 方法來建立命令物件。  
  
     命令物件會執行提供者支援的命令。 利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者，取用者可以指定任何 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，例如 SELECT 陳述式或預存程序的呼叫。 使用命令物件建立資料列集的步驟如下：  
  
    1.  取用者會呼叫工作階段上的 **IDBCreateCommand::CreateCommand** 方法來取得在命令物件上要求 **ICommandText** 介面的命令物件。 這個 **ICommandText** 介面會設定及擷取實際的命令文字。 取用者會呼叫 **ICommandText::SetCommandText** 方法來填入文字命令。  
  
    2.  使用者會針對命令呼叫 **ICommand::Execute** 方法。 命令執行時所建立的資料列集物件包含來自命令的結果集。  
  
 取用者可以使用 **ICommandProperties** 介面來取得或設定 **ICommand::Execute** 介面所執行之命令傳回的資料列集屬性。 最常要求的屬性為資料列集必須支援的介面。 除了介面之外，取用者可以要求修改資料列集或介面之行為的屬性。  
  
 取用者會使用 **IRowset::Release** 方法釋放資料列集。 釋放資料列集時，也會釋放取用者在該資料列集上保留的所有資料列控制代碼。 釋放資料列集不會釋放存取子。 如果您有 **IAccessor** 介面，仍然必須釋放該介面。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [以 IOpenRowset 建立資料列集](../../relational-databases/native-client-ole-db-rowsets/creating-a-rowset-with-iopenrowset.md)  
  
-   [使用 ICommand:: Execute 建立資料列集](../../relational-databases/native-client-ole-db-rowsets/creating-rowsets-with-icommand-execute.md)  
  
-   [資料列集屬性和行為](../../relational-databases/native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)  
  
-   [資料列集和 SQL Server 資料指標](../../relational-databases/native-client-ole-db-rowsets/rowsets-and-sql-server-cursors.md)  
  
-   [擷取資料列](../../relational-databases/native-client-ole-db-rowsets/fetching-rows.md)  
  
-   [使用 IRow 擷取單一資料列](../../relational-databases/native-client-ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
-   [書籤](../../relational-databases/native-client-ole-db-rowsets/bookmarks.md)  
  
-   [更新資料列集中的資料](../../relational-databases/native-client-ole-db-rowsets/updating-data-in-rowsets.md)  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
