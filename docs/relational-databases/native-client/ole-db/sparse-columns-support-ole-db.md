---
title: "疏鬆資料行支援 (OLE DB) |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 918574b3-c62e-4937-9e5f-37310dedc8f9
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e619df00ebd8c35d950de35aacc058f24205c2e6
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sparse-columns-support-ole-db"></a>疏鬆資料行支援 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  本主題提供 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 對於疏鬆資料行支援的相關資訊。 如需有關疏鬆資料行的詳細資訊，請參閱[SQL Server Native Client 中的疏鬆資料行支援](../../../relational-databases/native-client/features/sparse-columns-support-in-sql-server-native-client.md)。 如需範例，請參閱[顯示資料行與疏鬆資料行 &#40; OLE DB &#41; 的目錄中繼資料](../../../relational-databases/native-client-ole-db-how-to/display-column-and-catalog-metadata-for-sparse-columns-ole-db.md)。  
  
## <a name="ole-db-statement-metadata"></a>OLE DB 陳述式中繼資料  
 從 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 開始，提供新的 DBCOLUMNFLAGS 旗標值 DBCOLUMNFLAGS_SS_ISCOLUMNSET。 這個值應該設定的資料行**column_set**值。 DBCOLUMNFLAGS 旗標可以透過擷取*dwFlags* icolumnsinfo:: Getcolumnsinfo 和 icolumnsrowset:: Getcolumnsrowset 所傳回的資料列集的 DBCOLUMN_FLAGS 資料行的參數。  
  
## <a name="ole-db-catalog-metadata"></a>OLE DB 目錄中繼資料  
 系統已經將兩個額外的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 專用資料行加入到 DBSCHEMA_COLUMNS 中。  
  
|資料行名稱|資料類型|值/註解|  
|-----------------|---------------|---------------------|  
|SS_IS_SPARSE|DBTYPE_BOOL|如果資料行為疏鬆資料行，這個值為 VARIANT_TRUE，否則為 VARIANT_FALSE。|  
|SS_IS_COLUMN_SET|DBTYPE_BOOL|如果資料行是疏鬆**column_set**資料行，這會有值為 VARIANT_TRUE，否則 VARIANT_FALSE。|  
  
 系統也已經加入兩個額外的結構描述資料列集。 這些資料列集與 DBSCHEMA_COLUMNS 的結構相同，但傳回不同的內容。 DBSCHEMA_COLUMNS_EXTENDED 會傳回所有資料行，不論**column_set**成員資格。 DBSCHEMA_SPARSE_COLUMN_SET 傳回成員的疏鬆資料行**column_set**。  
  
## <a name="ole-db-datatypecompatibility-behavior"></a>OLE DB DataTypeCompatibility 行為  
 行為**DataTypeCompatibility = 80** （在連接字串） 是與一致[!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)]用戶端，如下所示：  
  
-   您看不到新的結構描述資料列集，而且在結構描述資料列集中沒有它們的資料列。  
  
-   您看不到 COLUMNS 資料列集中的新資料行。  
  
-   針對不會設定 DBCOLUMNFLAGS_SS_ISCOLUMNSET **column_set**資料行。  
  
-   資料行會設定 DBCOMPUTEMODE_NOTCOMPUTED **column_set**資料行。  
  
## <a name="ole-db-support-for-sparse-columns"></a>疏鬆資料行的 OLE DB 支援  
 下列 OLE DB 介面會在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 中修改以支援疏鬆資料行：  
  
|類型或成員函數|Description|  
|-----------------------------|-----------------|  
|Icolumnsinfo:: Getcolumnsinfo|新 DBCOLUMNFLAGS 旗標的值 DBCOLUMNFLAGS_SS_ISCOLUMNSET 設定**column_set**中的資料行*dwFlags*。<br /><br /> 資料行會設定 DBCOLUMNFLAGS_WRITE **column_set**資料行。|  
|IColumsRowset::GetColumnsRowset|設定新 DBCOLUMNFLAGS 旗標值 DBCOLUMNFLAGS_SS_ISCOLUMNSET **column_set** DBCOLUMN_FLAGS 中的資料行。<br /><br /> Dbcolumn_computemode 會設為 DBCOMPUTEMODE_DYNAMIC **column_set**資料行。|  
|IDBSchemaRowset::GetSchemaRowset|DBSCHEMA_COLUMNS 會傳回兩個新的資料行：SS_IS_COLUMN_SET 和 SS_IS_SPARSE。<br /><br /> DBSCHEMA_COLUMNS 會傳回不是成員的資料行**column_set**。<br /><br /> 已加入兩個新的結構描述資料列集： DBSCHEMA_COLUMNS_EXTENDED 將會傳回所有資料行的疏鬆度不論**column_set**成員資格。 DBSCHEMA_SPARSE_COLUMN_SET 傳回成員的資料行**column_set**。 這些新的資料列集與 DBSCHEMA_COLUMNS 的資料行和限制相同。|  
|Idbschemarowset:: Getschemas|Idbschemarowset:: Getschemas 可用結構描述資料列集的清單中包含新的資料列集 DBSCHEMA_COLUMNS_EXTENDED 和 DBSCHEMA_SPARSE_COLUMN_SET 的 Guid。|  
|ICommand::Execute|如果**選取\*從***資料表*是它使用，會傳回所有資料行不屬於疏鬆**column_set**，再加上包含的所有值的 XML 資料行非 null 資料行成員的疏鬆**column_set**，如果有的話。|  
|IOpenRowset::OpenRowset|傳回與 icommand:: Execute，相同的資料行的資料列集 iopenrowset:: Openrowset**選取\***相同資料表上的查詢。|  
|ITableDefinition|沒有任何變更，此介面為疏鬆資料行或**column_set**資料行。 需要修改結構描述的應用程式必須直接執行適當的 [!INCLUDE[tsql](../../../includes/tsql-md.md)]。|  
  
## <a name="see-also"></a>請參閱＜  
 [SQL Server Native Client &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
