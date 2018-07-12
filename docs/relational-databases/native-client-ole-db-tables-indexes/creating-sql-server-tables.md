---
title: 建立 SQL Server 資料表 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
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
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5809cf0f602072b0bf1174ded2ed2502f7d9c277
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2018
ms.locfileid: "37423927"
---
# <a name="creating-sql-server-tables"></a>建立 SQL Server 資料表
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會公開**itabledefinition:: Createtable**函式，讓取用者建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表。 取用者會使用**CreateTable**使用所產生的唯一名稱建立取用者命名的永久資料表，以及永久或暫存資料表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者。  
  
 當取用者呼叫**itabledefinition:: Createtable**，如果 DBPROP_TBL_TEMPTABLE 屬性的值為 VARIANT_TRUE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會產生取用者的暫存資料表名稱。 取用者集*Createtable*的參數**CreateTable**方法設為 NULL。 所產生之名稱的暫存資料表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者不會出現在**資料表**資料列集，但可透過存取**IOpenRowset**介面。  
  
 當取用者指定的資料表名稱*pwszName*隸屬*uName*聯集*pTableID*參數， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]具有該名稱的資料表。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表的命名條件約束便會套用，而且資料表名稱可以表示永久資料表，或者本機或全域暫存資料表。 如需詳細資訊，請參閱 < [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)。 *PpTableID*參數可以是 NULL。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者可以產生永久或暫存資料表的名稱。 當取用者設定*Createtable*參數為 NULL，而且集*ppTableID*指向有效的 DBID\*，則[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會傳回產生的名稱資料表中*pwszName*隸屬*uName* DBID 的聯集的值所指向*ppTableID*。 若要建立暫存[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者命名的資料表，取用者包含 OLE DB 資料表屬性 DBPROP_TBL_TEMPTABLE 設定中參考的資料表屬性*rgPropertySets*參數。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者命名的暫存資料表是本機。  
  
 **CreateTable**如果傳回 DB_E_BADTABLEID *eKind*隸屬*pTableID*參數不包含 dbkind_name。  
  
## <a name="dbcolumndesc-usage"></a>DBCOLUMNDESC 用法  
 取用者可以使用其中一種表示資料行資料類型*pwszTypeName*成員或*wType*成員。 如果取用者指定中的資料類型*pwszTypeName*，則[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會忽略的值*wType*。  
  
 如果使用*pwszTypeName*成員，取用者指定的資料類型使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料型別名稱。 有效的資料類型名稱是在 PROVIDER_TYPES 結構描述資料列集之 TYPE_NAME 資料行中傳回的資料類型名稱。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會在 OLE DB 列舉之 DBTYPE 值的子集*wType*成員。 如需詳細資訊，請參閱 < [ITableDefinition 中的資料類型對應](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-itabledefinition.md)。  
  
> [!NOTE]  
>  **CreateTable**如果取用者設定，會傳回 DB_E_BADTYPE *pTypeInfo*或是*createtable*來指定資料行資料類型的成員。  
  
 取用者指定的資料行名稱*pwszName*隸屬*uName*聯集之 DBCOLUMNDESC *dbcid*成員。 資料行名稱會指定為 Unicode 字元字串。 *EKind*隸屬*dbcid*必須是 DBKIND_NAME。 **CreateTable**傳回 DB_E_BADCOLUMNID *eKind*不正確、 此*pwszName*為 NULL，或如果的值*pwszName*不是有效[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]識別項。  
  
 在針對資料表定義的所有資料行上都可以使用所有資料行屬性。 **CreateTable**可以傳回 DB_S_ERRORSOCCURRED 或 DB_E_ERRORSOCCURRED 如果屬性值的設定發生衝突。 **CreateTable**會傳回無效的資料行屬性設定造成錯誤[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表建立失敗。  
  
 DBCOLUMNDESC 中的資料行屬性解譯如下。  
  
|屬性識別碼|描述|  
|-----------------|-----------------|  
|DBPROP_COL_AUTOINCREMENT|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE 描述：在建立的資料行上設定識別屬性。 對於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，識別屬性適用於資料表內的單一資料行。 將屬性設定為 VARIANT_TRUE，針對多個單一資料行就會產生錯誤時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會嘗試在伺服器上建立資料表。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Identity 屬性僅適用於**整數**，**數值**，和**decimal**類型小數位數為 0。 任何其他資料類型的資料行上將屬性設定為 VARIANT_TRUE 會產生錯誤時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會嘗試在伺服器上建立資料表。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者傳回 DB_S_ERRORSOCCURRED，當 DBPROP_COL_AUTOINCREMENT 和 DBPROP_COL_NULLABLE 同時為 VARIANT_TRUE， *dwOption* DBPROP_COL_NULLABLE 不 DBPROPOPTIONS_必要的。 當 DBPROP_COL_AUTOINCREMENT 和 DBPROP_COL_NULLABLE 同時為 VARIANT_TRUE 會傳回 DB_E_ERRORSOCCURRED， *dwOption* DBPROP_COL_NULLABLE 等於 dbpropoptions_required 時。 資料行定義[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]identity 屬性和 DBPROP_COL_NULLABLE *dwStatus*成員設定為 DBPROPSTATUS_CONFLICTING。|  
|DBPROP_COL_DEFAULT|R/W：讀取/寫入<br /><br /> 預設值：無<br /><br /> 描述：建立資料行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DEFAULT 條件約束。<br /><br /> *VValue* DBPROP 成員可以是任何類型的數目。 *VValue.vt*成員應該指定與資料行的資料類型相容的類型。 例如，對於定義為 DBTYPE_WSTR 的資料行而言，將 BSTR N/A 定義為預設值是相容符合。 定義為 DBTYPE_R8 會產生錯誤的資料行上定義相同的預設時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會嘗試在伺服器上建立資料表。|  
|DBPROP_COL_DESCRIPTION|R/W：讀取/寫入<br /><br /> 預設值：無<br /><br /> 描述： DBPROP_COL_DESCRIPTION 資料行屬性不會實作[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者。<br /><br /> *DwStatus* DBPROP 結構的成員會取用者嘗試寫入屬性值時，會傳回 DBPROPSTATUS_NOTSUPPORTED。<br /><br /> 將屬性設定不會構成嚴重錯誤[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者。 如果其他所有參數值都有效，則會建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。|  
|DBPROP_COL_FIXEDLENGTH|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會使用 DBPROP_COL_FIXEDLENGTH 來決定資料類型對應，取用者使用定義的資料行資料類型時*wType* DBCOLUMNDESC 的成員。 如需詳細資訊，請參閱 < [ITableDefinition 中的資料類型對應](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-itabledefinition.md)。|  
|DBPROP_COL_NULLABLE|R/W：讀取/寫入<br /><br /> 預設值：無<br /><br /> 描述： 建立資料表時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者會指出是否在設定屬性，資料行是否應該接受 null 值。 未設定屬性時，資料行是否能夠接受 NULL 做為值取決於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ANSI_NULLS 預設資料庫選項。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者是符合 ISO 的提供者。 已連接的工作階段會表現 ISO 行為。 如果取用者沒有設定 DBPROP_COL_NULLABLE，資料行接受 Null 值。|  
|DBPROP_COL_PRIMARYKEY|R/W：讀取/寫入<br /><br /> 預設值： VARIANT_FALSE 描述： 當 VARIANT_TRUE 時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會建立具有主索引鍵條件約束的資料行。<br /><br /> 定義為資料行屬性時，只有單一資料行可以決定條件約束。 設定屬性 VARIANT_TRUE 會針對多個單一資料行則會傳回錯誤時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者嘗試建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表。<br /><br /> 注意： 取用者可以使用**iindexdefinition:: Createindex**建立兩個或多個資料行上的主索引鍵條件約束。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者傳回 DB_S_ERRORSOCCURRED，當 DBPROP_COL_PRIMARYKEY 和 DBPROP_COL_UNIQUE 同時為 VARIANT_TRUE， *dwOption* DBPROP_COL_UNIQUE 不是 dbpropoptions_required 時。<br /><br /> 當 DBPROP_COL_PRIMARYKEY 和 DBPROP_COL_UNIQUE 同時為 VARIANT_TRUE 會傳回 DB_E_ERRORSOCCURRED， *dwOption* DBPROP_COL_UNIQUE 等於 dbpropoptions_required 時。 資料行定義[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]identity 屬性，而 DBPROP_COL_PRIMARYKEY *dwStatus*成員設定為 DBPROPSTATUS_CONFLICTING。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會傳回錯誤，當 DBPROP_COL_PRIMARYKEY 和 DBPROP_COL_NULLABLE 同時為 VARIANT_TRUE。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會傳回從錯誤[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]取用者嘗試建立無效的資料行上主索引鍵條件約束[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料型別。 無法使用建立的資料行上定義 PRIMARY KEY 條件約束[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料型別**位元**，**文字**， **ntext**，以及**映像**.|  
|DBPROP_COL_UNIQUE|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE 描述：將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UNIQUE 條件約束套用到資料行。<br /><br /> 定義為資料行屬性時，僅會在單一資料行上套用條件約束。 取用者可以使用**iindexdefinition:: Createindex**来套用的兩個或多個資料行的合計值上唯一的條件約束。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者傳回 DB_S_ERRORSOCCURRED，當 DBPROP_COL_PRIMARYKEY 和 DBPROP_COL_UNIQUE 同時為 VARIANT_TRUE， *dwOption*不是 dbpropoptions_required 時。<br /><br /> 當 DBPROP_COL_PRIMARYKEY 和 DBPROP_COL_UNIQUE 同時為 VARIANT_TRUE 會傳回 DB_E_ERRORSOCCURRED 並*dwOption*等於 dbpropoptions_required 時。 資料行定義[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]identity 屬性，而 DBPROP_COL_PRIMARYKEY *dwStatus*成員設定為 DBPROPSTATUS_CONFLICTING。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者傳回 DB_S_ERRORSOCCURRED，當 DBPROP_COL_NULLABLE 和 DBPROP_COL_UNIQUE 同時為 VARIANT_TRUE， *dwOption*不是 dbpropoptions_required 時。<br /><br /> 當 DBPROP_COL_NULLABLE 和 DBPROP_COL_UNIQUE 同時為 VARIANT_TRUE 會傳回 DB_E_ERRORSOCCURRED 並*dwOption*等於 dbpropoptions_required 時。 資料行定義[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]identity 屬性和 DBPROP_COL_NULLABLE *dwStatus*成員設定為 DBPROPSTATUS_CONFLICTING。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會傳回從錯誤[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]取用者嘗試建立無效的資料行的唯一條件約束[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料型別。 無法建立與資料行上定義 UNIQUE 條件約束[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**元**資料型別。|  
  
 當取用者呼叫**itabledefinition:: Createtable**，則[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者解譯資料表屬性，如下所示。  
  
|屬性識別碼|描述|  
|-----------------|-----------------|  
|DBPROP_TBL_TEMPTABLE|R/W：讀取/寫入<br /><br /> 預設值： VARIANT_FALSE 描述： 根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會建立由取用者命名的資料表。 當 VARIANT_TRUE 時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會產生取用者的暫存資料表名稱。 取用者集*Createtable*的參數**CreateTable**為 NULL。 *PpTableID*參數必須包含有效的指標。|  
  
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
  
  
