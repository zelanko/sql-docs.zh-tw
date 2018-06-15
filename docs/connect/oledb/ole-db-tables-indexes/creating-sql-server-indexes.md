---
title: 建立 SQL Server 索引 |Microsoft 文件
description: 建立使用 SQL Server 的 OLE DB 驅動程式的 SQL Server 索引
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- CreateIndex function
- constraints [OLE DB]
- OLE DB Driver for SQL Server, indexes
- indexes [OLE DB]
- adding indexes
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 9648462e65ed85b5a9652e193dc63d30059c0753
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35306867"
---
# <a name="creating-sql-server-indexes"></a>建立 SQL Server 索引
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQL Server OLE DB 驅動程式會公開**iindexdefinition:: Createindex**函式，讓取用者上，定義新的索引[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料表。  
  
 SQL Server OLE DB 驅動程式會建立資料表索引做為索引或條件約束。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會將建立條件約束的權限提供給資料表擁有者、資料庫擁有者，以及特定管理角色的成員。 根據預設，只有資料表擁有者可以建立資料表的索引。 因此，成功或失敗**CreateIndex**不是只在應用程式使用者的存取權限，但也在建立索引的類型而定。  
  
 取用者指定的資料表名稱中的 Unicode 字元字串*pwszName*隸屬*uName*聯集*Createtable*參數。 *EKind*隸屬*Createtable*必須是 DBKIND_NAME。  
  
 *PIndexID*參數可以是 NULL，而如果是，SQL Server OLE DB 驅動程式會建立索引的唯一名稱。 取用者可以藉由指定 DBID 的有效指標擷取的索引名稱*ppIndexID*參數。  
  
 取用者可以指定為 Unicode 字元字串中的索引名稱*pwszName*隸屬*uName*等位的*pIndexID*參數。 *EKind*隸屬*pIndexID*必須是 DBKIND_NAME。  
  
 取用者會指定依名稱參與索引的一或多個資料行。 每個 DBINDEXCOLUMNDESC 結構中使用**CreateIndex**、 *eKind*隸屬*Ekind*必須是 DBKIND_NAME。 資料行名稱指定為 Unicode 字元字串中*pwszName*隸屬*uName*聯集*Ekind*。  
  
 SQL Server OLE DB 驅動程式和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]值支援遞增順序在索引中。 如果取用者在任何 DBINDEXCOLUMNDESC 結構中指定 DBINDEX_COL_ORDER_DESC，SQL Server OLE DB 驅動程式會傳回 E_INVALIDARG。  
  
 **CreateIndex**會解譯索引屬性，如下所示。  
  
|屬性識別碼|描述|  
|-----------------|-----------------|  
|DBPROP_INDEX_AUTOUPDATE|R/W：讀取/寫入<br /><br /> 預設值：無<br /><br /> 描述： SQL Server OLE DB 驅動程式不支援這個屬性。 嘗試將屬性設定**CreateIndex**使 DB_S_ERRORSOCCURRED 傳回值。 *DwStatus*屬性結構成員表示 DBPROPSTATUS_BADVALUE。|  
|DBPROP_INDEX_CLUSTERED|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述：控制索引叢集。<br /><br /> VARIANT_TRUE: SQL Server OLE DB 驅動程式會嘗試建立叢集的索引上[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料表。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 在任何資料表上，最多支援一個叢集索引。<br /><br /> VARIANT_FALSE: SQL Server OLE DB 驅動程式會嘗試建立非叢集索引上[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料表。|  
|DBPROP_INDEX_FILLFACTOR|R/W：讀取/寫入<br /><br /> 預設值： 0<br /><br /> 描述：指定儲存所使用之索引頁的百分比。 如需詳細資訊，請參閱[CREATE INDEX](../../../t-sql/statements/create-index-transact-sql.md)。<br /><br /> 變數的類型為 VT_I4。 其值必須大於或等於 1 且小於或等於 100。|  
|DBPROP_INDEX_INITIALIZE|R/W：讀取/寫入<br /><br /> 預設值：無<br /><br /> 描述： SQL Server OLE DB 驅動程式不支援這個屬性。 嘗試將屬性設定**CreateIndex**使 DB_S_ERRORSOCCURRED 傳回值。 *DwStatus*屬性結構成員表示 DBPROPSTATUS_BADVALUE。|  
|DBPROP_INDEX_NULLCOLLATION|R/W：讀取/寫入<br /><br /> 預設值：無<br /><br /> 描述： SQL Server OLE DB 驅動程式不支援這個屬性。 嘗試將屬性設定**CreateIndex**使 DB_S_ERRORSOCCURRED 傳回值。 *DwStatus*屬性結構成員表示 DBPROPSTATUS_BADVALUE。|  
|DBPROP_INDEX_NULLS|R/W：讀取/寫入<br /><br /> 預設值：無<br /><br /> 描述： SQL Server OLE DB 驅動程式不支援這個屬性。 嘗試將屬性設定**CreateIndex**使 DB_S_ERRORSOCCURRED 傳回值。 *DwStatus*屬性結構成員表示 DBPROPSTATUS_BADVALUE。|  
|DBPROP_INDEX_PRIMARYKEY|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE 描述：建立索引做為參考完整性，也就是 PRIMARY KEY 條件約束。<br /><br /> VARIANT_TRUE：索引建立之後，即可支援資料表的 PRIMARY KEY 條件約束。 資料行必須是不允許為 Null。<br /><br /> VARIANT_FALSE：索引不會當做資料表中之資料列值的 PRIMARY KEY 條件約束使用。|  
|DBPROP_INDEX_SORTBOOKMARKS|R/W：讀取/寫入<br /><br /> 預設值：無<br /><br /> 描述： SQL Server OLE DB 驅動程式不支援這個屬性。 嘗試將屬性設定**CreateIndex**使 DB_S_ERRORSOCCURRED 傳回值。 *DwStatus*屬性結構成員表示 DBPROPSTATUS_BADVALUE。|  
|DBPROP_INDEX_TEMPINDEX|R/W：讀取/寫入<br /><br /> 預設值：無<br /><br /> 描述： SQL Server OLE DB 驅動程式不支援這個屬性。 嘗試將屬性設定**CreateIndex**使 DB_S_ERRORSOCCURRED 傳回值。 *DwStatus*屬性結構成員表示 DBPROPSTATUS_BADVALUE。|  
|DBPROP_INDEX_TYPE|R/W：讀取/寫入<br /><br /> 預設值：無<br /><br /> 描述： SQL Server OLE DB 驅動程式不支援這個屬性。 嘗試將屬性設定**CreateIndex**使 DB_S_ERRORSOCCURRED 傳回值。 *DwStatus*屬性結構成員表示 DBPROPSTATUS_BADVALUE。|  
|DBPROP_INDEX_UNIQUE|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述：建立索引做為參與之一或多個資料行的 UNIQUE 條件約束。<br /><br /> VARIANT_TRUE：此索引用於唯一限制資料表中的資料列值。<br /><br /> VARIANT_FALSE：此索引不會唯一限制資料列值。|  
  
 在提供者特有的屬性集 DBPROPSET_SQLSERVERINDEX 中，SQL Server OLE DB 驅動程式會定義下列資料來源資訊屬性。  
  
|屬性識別碼|描述|  
|-----------------|-----------------|  
|SSPROP_INDEX_XML|類型：VT_BOOL (R/W)<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述：利用包含 IIndexDefinition::CreateIndex 的 VARIANT_TRUE 值指定此屬性時，會建立對應到要建立索引之資料行的主要 xml 索引。 如果此屬性為 VARIANT_TRUE，cIndexColumnDescs 應該為 1，否則就是錯誤。|  
  
 此範例會建立一個主索引鍵索引：  
  
```  
// This CREATE TABLE statement shows the referential integrity and   
// PRIMARY KEY constraint on the OrderDetails table that will be created   
// by the following example code.  
//  
// CREATE TABLE OrderDetails  
// (  
//    OrderID      int      NOT NULL  
//    ProductID   int      NOT NULL  
//        CONSTRAINT PK_OrderDetails  
//        PRIMARY KEY CLUSTERED (OrderID, ProductID),  
//    UnitPrice   money      NOT NULL,  
//    Quantity   int      NOT NULL,  
//    Discount   decimal(2,2)   NOT NULL  
//        DEFAULT 0  
// )  
//  
HRESULT CreatePrimaryKey  
    (  
    IIndexDefinition* pIIndexDefinition  
    )  
    {  
    HRESULT             hr = S_OK;  
  
    DBID                dbidTable;  
    DBID                dbidIndex;  
    const ULONG         nCols = 2;  
    ULONG               nCol;  
    const ULONG         nProps = 2;  
    ULONG               nProp;  
  
    DBINDEXCOLUMNDESC   dbidxcoldesc[nCols];  
    DBPROP              dbpropIndex[nProps];  
    DBPROPSET           dbpropset;  
  
    DBID*               pdbidIndexOut = NULL;  
  
    // Set up identifiers for the table and index.  
    dbidTable.eKind = DBKIND_NAME;  
    dbidTable.uName.pwszName = L"OrderDetails";  
  
    dbidIndex.eKind = DBKIND_NAME;  
    dbidIndex.uName.pwszName = L"PK_OrderDetails";  
  
    // Set up column identifiers.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        dbidxcoldesc[nCol].pColumnID = new DBID;  
        dbidxcoldesc[nCol].pColumnID->eKind = DBKIND_NAME;  
  
        dbidxcoldesc[nCol].eIndexColOrder = DBINDEX_COL_ORDER_ASC;  
        }  
    dbidxcoldesc[0].pColumnID->uName.pwszName = L"OrderID";  
    dbidxcoldesc[1].pColumnID->uName.pwszName = L"ProductID";  
  
    // Set properties for the index. The index is clustered,  
    // PRIMARY KEY.  
    for (nProp = 0; nProp < nProps; nProp++)  
        {  
        dbpropIndex[nProp].dwOptions = DBPROPOPTIONS_REQUIRED;  
        dbpropIndex[nProp].colid = DB_NULLID;  
  
        VariantInit(&(dbpropIndex[nProp].vValue));  
  
        dbpropIndex[nProp].vValue.vt = VT_BOOL;  
        }  
    dbpropIndex[0].dwPropertyID = DBPROP_INDEX_CLUSTERED;  
    dbpropIndex[0].vValue.boolVal = VARIANT_TRUE;  
  
    dbpropIndex[1].dwPropertyID = DBPROP_INDEX_PRIMARYKEY;  
    dbpropIndex[1].vValue.boolVal = VARIANT_TRUE;  
  
    dbpropset.rgProperties = dbpropIndex;  
    dbpropset.cProperties = nProps;  
    dbpropset.guidPropertySet = DBPROPSET_INDEX;  
  
    hr = pIIndexDefinition->CreateIndex(&dbidTable, &dbidIndex, nCols,  
        dbidxcoldesc, 1, &dbpropset, &pdbidIndexOut);  
  
    // Clean up dynamically allocated DBIDs.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        delete dbidxcoldesc[nCol].pColumnID;  
        }  
  
    return (hr);  
    }  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料表和索引](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)  
  
  
