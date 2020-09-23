---
title: OLE DB Driver for SQL Server 中的疏鬆資料行支援 | Microsoft Docs
description: 了解 OLE DB Driver for SQL Server 如何支援疏鬆資料行，並查看 SQL Server 中疏鬆資料行的相關資訊。
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- sparse columns, OLE DB Driver for SQL Server
- sparse columns, OLE DB
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1397d69f72cfc1362decf84959046d581befea5b
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862284"
---
# <a name="sparse-columns-support-in-ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server 中的疏鬆資料行支援
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 支援疏鬆資料行。 如需有關 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中疏鬆資料行的詳細資訊，請參閱[使用疏鬆資料行](../../../relational-databases/tables/use-sparse-columns.md)和[使用資料行集](../../../relational-databases/tables/use-column-sets.md)。  
  
 如需有關 OLE DB Driver for SQL Server 中疏鬆資料行支援的詳細資訊，請參閱[疏鬆資料行支援 &#40;OLE DB&#41;](../../oledb/ole-db/sparse-columns-support-ole-db.md)。  
  
 如需示範這項功能之範例應用程式的詳細資訊，請參閱 [SQL Server 資料程式設計範例](https://msftdpprodsamples.codeplex.com/)。  
  
## <a name="user-scenarios-for-sparse-columns-and-ole-db-driver-for-sql-server"></a>疏鬆資料行與 OLE DB Driver for SQL Server 的使用者案例  
 下表針對包含疏鬆資料行的 OLE DB Driver for SQL Server 使用者摘要說明一般使用者案例：  
  
|狀況|行為|  
|--------------|--------------|  
|**從資料表**或 IOpenRowset::OpenRowset 選取 \*。|傳回不屬於疏鬆 **column_set** 成員的所有資料行，加上包含屬於疏鬆 **column_set** 成員之所有非 Null 資料行值的 XML 資料行。|  
|依名稱參考資料行。|不管其疏鬆資料行狀態或 **column_set** 成員資格，都可以參考資料行。|  
|透過計算 XML 資料行，存取 **column_set** 成員資料行。|屬於疏鬆 **column_set** 成員的資料行可以透過依名稱選取 **column_set** 來存取，而且可以透過更新 **column_set** 資料行中的 XML 來插入和更新值。<br /><br /> 這個值必須符合 **column_set** 資料行的結構描述。|  
|透過沒有資料行限制 (OLE DB) 的 DBSCHEMA_COLUMNS 結構描述資料列集，擷取資料表中所有資料行的中繼資料。|傳回不屬於疏鬆 **column_set** 成員之所有資料行的資料列。 如果資料表包含疏鬆 **column_set**，將會針對該資料表傳回一個資料列。<br /><br /> 請注意，這不會針對屬於 **column_set** 成員的資料行傳回中繼資料。|  
|不管 **column_set** 中的疏鬆度或成員資格，擷取所有資料行的中繼資料。 這可能會傳回非常大量的資料列。|針對 DBSCHEMA_COLUMNS_EXTENDED 結構描述資料列集呼叫 IDBSchemaRowset::GetRowset。|  
|僅針對屬於 **column_set** 成員的資料行擷取中繼資料。 這可能會傳回非常大量的資料列。|針對 DBSCHEMA_SPARSE_COLUMN_SET 結構描述資料列集呼叫 IDBSchemaRowset::GetRowset。|  
|決定資料行是否為疏鬆。|查閱 DBSCHEMA_COLUMNS 結構描述資料列集 (OLE DB) 的 SS_IS_SPARSE 資料行。|  
|判斷資料行是否為 **column_set**。|查閱 DBSCHEMA_COLUMNS 結構描述資料列集的 SS_IS_COLUMN_SET 資料行。 或者，查閱 IColumnsRowset::GetColumnsRowset 所傳回的資料列集中 IColumnsinfo::GetColumnInfo 或 DBCOLUMNFLAGS 傳回的 *dwFlags*。 針對 **column_set** 資料行，將會設定 DBCOLUMNFLAGS_SS_ISCOLUMNSET。|  
|針對沒有 **column_set** 的資料表，依 BCP 匯入和匯出疏鬆資料行。|從舊版 OLE DB Driver for SQL Server 開始，沒有行為上的變更。|  
|針對包含 **column_set** 的資料表，依 BCP 匯入和匯出疏鬆資料行。|**column_set** 的匯入和匯出方式與 XML 相同；也就是說，如果當作二進位類型繫結，如同 **varbinary(max)**，或者，如果當作 **char** 或 **wchar** 類型繫結，則如同 **nvarchar(max)**。<br /><br /> 屬於疏鬆 **column_set** 成員的資料行不會匯出為不同的資料行；它們只會在 **column_set** 的值中匯出。|  
|BCP 的 **queryout** 行為。|從舊版 OLE DB Driver for SQL Server 開始，在明確具名的資料行處理上沒有變更。<br /><br /> 與包含不同結構描述之資料表間匯入和匯出相關的案例可能需要特殊處理。<br /><br /> 如需有關 BCP 的詳細資訊，請參閱本主題稍後的「疏鬆資料行的大量複製 (BCP) 支援」。|  
  
## <a name="down-level-client-behavior"></a>下層用戶端行為  
 下層用戶端僅會針對不屬於 SQLColumns 和 DBSCHMA_COLUMNS 之疏鬆 **column_set** 成員的資料行傳回中繼資料。
  
 下層用戶端可以依名稱存取屬於疏鬆 **column_set** 成員的資料行，而且 **column_set** 資料行將可以存取 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 用戶端的 XML 資料行。  
  
## <a name="bulk-copy-bcp-support-for-sparse-columns"></a>疏鬆資料行的大量複製 (BCP) 支援  
 在 OLE DB 中，沒有針對疏鬆資料行或 **column_set** 功能的 BCP API 變更。  
  
 如果某個資料表包含 **column_set**，則不會將疏鬆資料行當作不同的資料行處理。 所有疏鬆資料行的值都包含在 **column_set** 的值中，其匯出方式與 XML 資料行相同，也就是說，如果當作二進位類型繫結，如同 **varbinary(max)**，或者，如果當作 **char** 或 **wchar** 類型繫結，則如同 **nvarchar(max)**。 匯入時，**column_set** 值必須符合 **column_set** 的結構描述。  
  
 針對 **queryout** 作業，不會變更處理明確參考之資料行的方式。 **column_set** 資料行的行為與 XML 資料行相同，而且疏鬆度對於具名疏鬆資料行的處理沒有作用。  
  
 不過，如果 **queryout** 用於匯出，而且您參考的疏鬆資料行屬於依名稱設定之疏鬆資料行集的成員，則您無法直接匯入結構類似的資料表。 這是因為 BCP 會在匯出時使用與 **select \*** 作業一致的中繼資料，而且無法將 **column_set** 成員資料行與此中繼資料比對。 若要個別匯入 **column_set** 成員資料行，您必須在資料表上定義參考所需 **column_set** 資料行的檢視表，而且您必須使用檢視表執行匯入作業。  
  
## <a name="see-also"></a>另請參閱  
 [OLE DB Driver for SQL Server](../../oledb/oledb-driver-for-sql-server.md)  
  
  
