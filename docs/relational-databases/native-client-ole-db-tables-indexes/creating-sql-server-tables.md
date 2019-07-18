---
title: 建立 SQL Server 資料表 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- tables [OLE DB]
- SQL Server Native Client OLE DB provider, tables
- DBCOLUMNDESC usage
- adding tables
- CreateTable function
ms.assetid: a7b8d142-d76a-44d9-a583-86ac5109fbe8
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 72a278a142889d8b9d1e43976939f06b002689d7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069739"
---
# <a name="creating-sql-server-tables"></a>建立 SQL Server 資料表
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會公開**itabledefinition:: Createtable**函式，讓取用者建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表。 取用者會使用**CreateTable**使用所產生的唯一名稱建立取用者命名的永久資料表，以及永久或暫存資料表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者。  
  
 當取用者呼叫**itabledefinition:: Createtable**，如果 DBPROP_TBL_TEMPTABLE 屬性的值為 VARIANT_TRUE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會產生取用者的暫存資料表名稱。 取用者會將 **CreateTable** 方法的 *pTableID* 參數設定為 NULL。 所產生之名稱的暫存資料表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者不會出現在**資料表**資料列集，但可透過存取**IOpenRowset**介面。  
  
 當取用者指定的資料表名稱*pwszName*隸屬*uName*聯集*pTableID*參數， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]具有該名稱的資料表。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表的命名條件約束便會套用，而且資料表名稱可以表示永久資料表，或者本機或全域暫存資料表。 如需詳細資訊，請參閱 [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)。 *ppTableID* 參數可以是 NULL。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者可以產生永久或暫存資料表的名稱。 當取用者設定*Createtable*參數為 NULL，而且集*ppTableID*指向有效的 DBID\*，則[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會傳回產生的名稱資料表中*pwszName*隸屬*uName* DBID 的聯集的值所指向*ppTableID*。 若要建立暫存[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者命名的資料表，取用者包含 OLE DB 資料表屬性 DBPROP_TBL_TEMPTABLE 設定中參考的資料表屬性*rgPropertySets*參數。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者命名的暫存資料表是本機。  
  
 如果 **pTableID** 參數的 *eKind* 成員不包含 DBKIND_NAME，*CreateTable* 會傳回 DB_E_BADTABLEID。  
  
## <a name="dbcolumndesc-usage"></a>DBCOLUMNDESC 用法  
 取用者可以使用 *pwszTypeName* 成員或 *wType* 成員來指出資料行資料類型。 如果取用者指定中的資料類型*pwszTypeName*，則[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會忽略的值*wType*。  
  
 如果使用 *pwszTypeName* 成員，取用者會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型名稱指定資料類型。 有效的資料類型名稱是在 PROVIDER_TYPES 結構描述資料列集之 TYPE_NAME 資料行中傳回的資料類型名稱。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會在 OLE DB 列舉之 DBTYPE 值的子集*wType*成員。 如需詳細資訊，請參閱 < [ITableDefinition 中的資料類型對應](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-itabledefinition.md)。  
  
> [!NOTE]  
>  如果取用者將 *pTypeInfo* 或 *pclsid* 成員設定為指定資料行資料類型，**CreateTable** 會傳回 DB_E_BADTYPE。  
  
 取用者會在 DBCOLUMNDESC *dbcid* 成員之 *uName* 聯集的 *pwszName* 成員中，指定資料行名稱。 資料行名稱會指定為 Unicode 字元字串。 *dbcid* 的 *eKind* 成員必須是 DBKIND_NAME。 如果 *eKind* 無效、*pwszName* 為 NULL，或者 *pwszName* 的值不是有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別碼，**CreateTable** 會傳回 DB_E_BADCOLUMNID。  
  
 在針對資料表定義的所有資料行上都可以使用所有資料行屬性。 如果屬性值的設定發生衝突，**CreateTable** 可能會傳回 DB_S_ERRORSOCCURRED 或 DB_E_ERRORSOCCURRED。 當無效的資料行屬性設定造成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表建立失敗時，**CreateTable** 會傳回錯誤。  
  
 DBCOLUMNDESC 中的資料行屬性解譯如下。  
  
|屬性識別碼|描述|  
|-----------------|-----------------|  
|DBPROP_COL_AUTOINCREMENT|R/W:讀取/寫入<br /><br /> 預設：VARIANT_FALSE 描述：建立資料行上設定 identity 屬性。 對於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，識別屬性適用於資料表內的單一資料行。 將屬性設定為 VARIANT_TRUE，針對多個單一資料行就會產生錯誤時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會嘗試在伺服器上建立資料表。<br /><br /> 當小數位數為 0 時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別屬性僅適用於 **integer**、**numeric** 和 **decimal** 類型。 任何其他資料類型的資料行上將屬性設定為 VARIANT_TRUE 會產生錯誤時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會嘗試在伺服器上建立資料表。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者傳回 DB_S_ERRORSOCCURRED，當 DBPROP_COL_AUTOINCREMENT 和 DBPROP_COL_NULLABLE 同時為 VARIANT_TRUE， *dwOption* DBPROP_COL_NULLABLE 不 DBPROPOPTIONS_必要的。 當 DBPROP_COL_AUTOINCREMENT 和 DBPROP_COL_NULLABLE 同時為 VARIANT_TRUE，而且 DBPROP_COL_NULLABLE 的 *dwOption* 等於 DBPROPOPTIONS_REQUIRED 時，會傳回 DB_E_ERRORSOCCURRED。 資料行會以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別屬性定義，而 DBPROP_COL_NULLABLE *dwStatus* 成員會設定為 DBPROPSTATUS_CONFLICTING。|  
|DBPROP_COL_DEFAULT|R/W:讀取/寫入<br /><br /> 預設：None<br /><br /> 描述：建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料行的 DEFAULT 條件約束。<br /><br /> *vValue* DBPROP 成員可以是任何一種類型。 *vValue.vt* 成員應該指定一個與資料行資料類型相容的類型。 例如，對於定義為 DBTYPE_WSTR 的資料行而言，將 BSTR N/A 定義為預設值是相容符合。 定義為 DBTYPE_R8 會產生錯誤的資料行上定義相同的預設時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會嘗試在伺服器上建立資料表。|  
|DBPROP_COL_DESCRIPTION|R/W:讀取/寫入<br /><br /> 預設：None<br /><br /> 描述：不會實作 DBPROP_COL_DESCRIPTION 資料行屬性[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者。<br /><br /> 當取用者嘗試寫入屬性值時，DBPROP 結構的 *dwStatus* 成員會傳回 DBPROPSTATUS_NOTSUPPORTED。<br /><br /> 將屬性設定不會構成嚴重錯誤[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者。 如果其他所有參數值都有效，則會建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。|  
|DBPROP_COL_FIXEDLENGTH|R/W:讀取/寫入<br /><br /> 預設：VARIANT_FALSE<br /><br /> 描述：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會使用 DBPROP_COL_FIXEDLENGTH 來決定資料類型對應，取用者使用定義的資料行資料類型時*wType* DBCOLUMNDESC 的成員。 如需詳細資訊，請參閱 < [ITableDefinition 中的資料類型對應](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-itabledefinition.md)。|  
|DBPROP_COL_NULLABLE|R/W:讀取/寫入<br /><br /> 預設：None<br /><br /> 描述：建立資料表時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會指出是否在設定屬性，資料行是否應該接受 null 值。 未設定屬性時，資料行是否能夠接受 NULL 做為值取決於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ANSI_NULLS 預設資料庫選項。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者是符合 ISO 的提供者。 已連接的工作階段會表現 ISO 行為。 如果取用者沒有設定 DBPROP_COL_NULLABLE，資料行接受 Null 值。|  
|DBPROP_COL_PRIMARYKEY|R/W:讀取/寫入<br /><br /> 預設：VARIANT_FALSE 描述：當 VARIANT_TRUE 時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會建立具有主索引鍵條件約束的資料行。<br /><br /> 定義為資料行屬性時，只有單一資料行可以決定條件約束。 設定屬性 VARIANT_TRUE 會針對多個單一資料行則會傳回錯誤時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者嘗試建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表。<br /><br /> 注意:取用者可以使用**iindexdefinition:: Createindex**建立兩個或多個資料行上的主索引鍵條件約束。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者傳回 DB_S_ERRORSOCCURRED，當 DBPROP_COL_PRIMARYKEY 和 DBPROP_COL_UNIQUE 同時為 VARIANT_TRUE， *dwOption* DBPROP_COL_UNIQUE 不是 dbpropoptions_required 時。<br /><br /> 當 DBPROP_COL_PRIMARYKEY 和 DBPROP_COL_UNIQUE 同時為 VARIANT_TRUE，而且 DBPROP_COL_UNIQUE 的 *dwOption* 等於 DBPROPOPTIONS_REQUIRED 時，會傳回 DB_E_ERRORSOCCURRED。 資料行會以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別屬性定義，而 DBPROP_COL_PRIMARYKEY *dwStatus* 成員會設定為 DBPROPSTATUS_CONFLICTING。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會傳回錯誤，當 DBPROP_COL_PRIMARYKEY 和 DBPROP_COL_NULLABLE 同時為 VARIANT_TRUE。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會傳回從錯誤[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]取用者嘗試建立無效的資料行上主索引鍵條件約束[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料型別。 在使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型 **bit**、**text**、**ntext** 和 **image** 建立的資料行上，無法定義 PRIMARY KEY 條件約束。|  
|DBPROP_COL_UNIQUE|R/W:讀取/寫入<br /><br /> 預設：VARIANT_FALSE 描述：適用於[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]UNIQUE 條件約束的資料行。<br /><br /> 定義為資料行屬性時，僅會在單一資料行上套用條件約束。 取用者可以使用 **IIndexDefinition::CreateIndex**，在結合兩個或多個資料行的值上套用 UNIQUE 條件約束。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者傳回 DB_S_ERRORSOCCURRED，當 DBPROP_COL_PRIMARYKEY 和 DBPROP_COL_UNIQUE 同時為 VARIANT_TRUE， *dwOption*不是 dbpropoptions_required 時。<br /><br /> 當 DBPROP_COL_PRIMARYKEY 和 DBPROP_COL_UNIQUE 同時為 VARIANT_TRUE，而且 *dwOption* 等於 DBPROPOPTIONS_REQUIRED 時，會傳回 DB_E_ERRORSOCCURRED。 資料行會以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別屬性定義，而 DBPROP_COL_PRIMARYKEY *dwStatus* 成員會設定為 DBPROPSTATUS_CONFLICTING。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者傳回 DB_S_ERRORSOCCURRED，當 DBPROP_COL_NULLABLE 和 DBPROP_COL_UNIQUE 同時為 VARIANT_TRUE， *dwOption*不是 dbpropoptions_required 時。<br /><br /> 當 DBPROP_COL_NULLABLE 和 DBPROP_COL_UNIQUE 同時為 VARIANT_TRUE，而且 *dwOption* 等於 DBPROPOPTIONS_REQUIRED 時，會傳回 DB_E_ERRORSOCCURRED。 資料行會以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別屬性定義，而 DBPROP_COL_NULLABLE *dwStatus* 成員會設定為 DBPROPSTATUS_CONFLICTING。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會傳回從錯誤[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]取用者嘗試建立無效的資料行的唯一條件約束[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料型別。 在使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bit** 資料類型建立的資料行上，無法定義 UNIQUE 條件約束。|  
  
 當取用者呼叫**itabledefinition:: Createtable**，則[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者解譯資料表屬性，如下所示。  
  
|屬性識別碼|描述|  
|-----------------|-----------------|  
|DBPROP_TBL_TEMPTABLE|R/W:讀取/寫入<br /><br /> 預設：VARIANT_FALSE 描述：根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會建立由取用者命名的資料表。 當 VARIANT_TRUE 時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會產生取用者的暫存資料表名稱。 取用者會將 **CreateTable** 的 *pTableID* 參數設定為 NULL。 *ppTableID* 參數必須包含有效的指標。|  
  
 如果取用者要求在成功建立的資料表上開啟的資料列集[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會開啟資料指標支援資料列集。 在傳遞的屬性集中可以指出任何資料列集屬性。  
  
 此範例會建立一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。  
  
```  
// This CREATE TABLE statement shows the details of the table created by   
// the following example code.  
//  
// CREATE TABLE OrderDetails  
// (  
//    OrderID      int      NOT NULL  
//    ProductID   int      NOT NULL  
//    CONSTRAINT PK_OrderDetails  
//         PRIMARY KEY CLUSTERED (OrderID, ProductID),  
//    UnitPrice   money      NOT NULL,  
//    Quantity   int      NOT NULL,  
//    Discount   decimal(2,2)   NOT NULL  
//        DEFAULT 0  
// )  
//  
// The PRIMARY KEY constraint is created in an additional example.  
HRESULT CreateTable  
    (  
    ITableDefinition* pITableDefinition  
    )  
    {  
    DBID            dbidTable;  
    const ULONG     nCols = 5;  
    ULONG           nCol;  
    ULONG           nProp;  
    DBCOLUMNDESC    dbcoldesc[nCols];  
  
    HRESULT         hr;  
  
    // Set up column descriptions. First, set default property values for  
    //  the columns.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        dbcoldesc[nCol].pwszTypeName = NULL;  
        dbcoldesc[nCol].pTypeInfo = NULL;  
        dbcoldesc[nCol].rgPropertySets = new DBPROPSET;  
        dbcoldesc[nCol].pclsid = NULL;  
        dbcoldesc[nCol].cPropertySets = 1;  
        dbcoldesc[nCol].ulColumnSize = 0;  
        dbcoldesc[nCol].dbcid.eKind = DBKIND_NAME;  
        dbcoldesc[nCol].wType = DBTYPE_I4;  
        dbcoldesc[nCol].bPrecision = 0;  
        dbcoldesc[nCol].bScale = 0;  
  
        dbcoldesc[nCol].rgPropertySets[0].rgProperties =   
            new DBPROP[NCOLPROPS_MAX];  
        dbcoldesc[nCol].rgPropertySets[0].cProperties = NCOLPROPS_MAX;  
        dbcoldesc[nCol].rgPropertySets[0].guidPropertySet =  
            DBPROPSET_COLUMN;  
  
        for (nProp = 0; nProp < NCOLPROPS_MAX; nProp++)  
            {  
            dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                dwOptions = DBPROPOPTIONS_REQUIRED;  
            dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].colid  
                 = DB_NULLID;  
  
            VariantInit(  
                &(dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                    vValue));  
  
            dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                vValue.vt = VT_BOOL;  
            }  
        }  
  
    // Set the column-specific information.  
    dbcoldesc[0].dbcid.uName.pwszName = L"OrderID";  
    dbcoldesc[0].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[0].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[0].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[1].dbcid.uName.pwszName = L"ProductID";  
    dbcoldesc[1].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[1].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[1].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[2].dbcid.uName.pwszName = L"UnitPrice";  
    dbcoldesc[2].wType = DBTYPE_CY;  
    dbcoldesc[2].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[2].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[2].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[3].dbcid.uName.pwszName = L"Quantity";  
    dbcoldesc[3].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[3].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[3].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[4].dbcid.uName.pwszName = L"Discount";  
    dbcoldesc[4].wType = DBTYPE_NUMERIC;  
    dbcoldesc[4].bPrecision = 2;  
    dbcoldesc[4].bScale = 2;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[1].dwPropertyID =   
        DBPROP_COL_DEFAULT;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[1].vValue.vt = VT_BSTR;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[1].vValue.bstrVal =  
        SysAllocString(L"0");  
    dbcoldesc[4].rgPropertySets[0].cProperties = 2;  
  
    // Set up the dbid for OrderDetails.  
    dbidTable.eKind = DBKIND_NAME;  
    dbidTable.uName.pwszName = L"OrderDetails";  
  
    if (FAILED(hr = pITableDefinition->CreateTable(NULL, &dbidTable,  
        nCols, dbcoldesc, NULL, 0, NULL, NULL, NULL)))  
        {  
        DumpError(pITableDefinition, IID_ITableDefinition);  
        goto SAFE_EXIT;  
        }  
  
SAFE_EXIT:  
    // Clean up dynamic allocation in the property sets.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        for (nProp = 0; nProp < NCOLPROPS_MAX; nProp++)  
            {  
            if (dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                vValue.vt == VT_BSTR)  
                {  
                SysFreeString(dbcoldesc[nCol].rgPropertySets[0].  
                    rgProperties[nProp].vValue.bstrVal);  
                }  
            }  
  
        delete [] dbcoldesc[nCol].rgPropertySets[0].rgProperties;  
        delete [] dbcoldesc[nCol].rgPropertySets;  
        }  
  
    return (hr);  
    }  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料表和索引](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
  
