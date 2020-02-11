---
title: 建立 SQL Server 資料表 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: e780a04f59bacba5063ac0bd6e9b7f3c74fd211a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "63046372"
---
# <a name="creating-sql-server-tables"></a>建立 SQL Server 資料表
  Native Client OLE DB 提供者會公開**ITableDefinition：： CreateTable**函數，讓取用者建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 取用者會使用**CreateTable**來建立取用者命名的永久資料表，以及包含 Native Client OLE DB 提供者所[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]產生之唯一名稱的永久或臨時表。  
  
 當取用者呼叫**ITableDefinition：： CreateTable**時，如果 DBPROP_TBL_TEMPTABLE 屬性的值為 VARIANT_TRUE， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會產生取用者的臨時表名稱。 取用者會將 *CreateTable* 方法的 **pTableID** 參數設定為 NULL。 具有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者所產生之名稱的臨時表不會出現在**tables**資料列集中，但是可以透過**IOpenRowset**介面存取。  
  
 當取用者在*pTableID*參數中，于*uName*聯集的*pwszName*成員中指定資料表名稱時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，Native Client OLE DB 提供者[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會建立具有該名稱的資料表。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表的命名條件約束便會套用，而且資料表名稱可以表示永久資料表，或者本機或全域暫存資料表。 如需詳細資訊，請參閱 [CREATE TABLE](/sql/t-sql/statements/create-table-transact-sql)。 
  *ppTableID* 參數可以是 NULL。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者可以產生永久資料表或臨時表的名稱。 當取用者將*pTableID*參數設定為 Null，並*將 ppTableID*設定為指向有效的\*DBID 時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，Native Client OLE DB 提供者會在*ppTableID*的*值所指向*的 DBID 的*pwszName*成員中，傳回所產生之資料表的名稱。 若要建立暫存的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者命名的資料表，取用者會在*rgPropertySets*參數中所參考的資料表屬性集內加入 OLE DB 資料表屬性 DBPROP_TBL_TEMPTABLE。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者命名的臨時表是本機的。  
  
 如果*pTableID*參數的*eKind*成員未指出 DBKIND_NAME，則**CreateTable**會傳回 DB_E_BADTABLEID。  
  
## <a name="dbcolumndesc-usage"></a>DBCOLUMNDESC 用法  
 取用者可以使用 *pwszTypeName* 成員或 *wType* 成員來指出資料行資料類型。 如果取用者在*pwszTypeName*中指定資料類型， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會忽略*wType*的值。  
  
 如果使用 *pwszTypeName* 成員，取用者會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型名稱指定資料類型。 有效的資料類型名稱是在 PROVIDER_TYPES 結構描述資料列集之 TYPE_NAME 資料行中傳回的資料類型名稱。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會辨識*wType*成員中 OLE DB 列舉之 DBTYPE 值的子集。 如需詳細資訊，請參閱[ITableDefinition 中的資料類型對應](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-itabledefinition.md)。  
  
> [!NOTE]  
>  如果取用者將*pTypeInfo*或*pclsid*成員設定為指定資料行資料類型，則**CreateTable**會傳回 DB_E_BADTYPE。  
  
 取用者會在 DBCOLUMNDESC *dbcid* 成員之 *uName* 聯集的 *pwszName* 成員中，指定資料行名稱。 資料行名稱會指定為 Unicode 字元字串。 
  *dbcid* 的 *eKind* 成員必須是 DBKIND_NAME。 如果*eKind*無效、 *pwszName*為 Null，或*pwszName*的值不是有效[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的識別碼，則**CreateTable**會傳回 DB_E_BADCOLUMNID。  
  
 在針對資料表定義的所有資料行上都可以使用所有資料行屬性。 如果屬性值在衝突中設定， **CreateTable**可以傳回 DB_S_ERRORSOCCURRED 或 DB_E_ERRORSOCCURRED。 **** 當不正確資料行屬性設定造成資料表建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]失敗時，CreateTable 會傳回錯誤。  
  
 DBCOLUMNDESC 中的資料行屬性解譯如下。  
  
|屬性識別碼|描述|  
|-----------------|-----------------|  
|DBPROP_COL_AUTOINCREMENT|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE 描述：在建立的資料行上設定識別屬性。 對於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，識別屬性適用於資料表內的單一資料行。 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者嘗試在伺服器上建立資料表時，針對多個單一資料行將屬性設定為 VARIANT_TRUE 會產生錯誤。<br /><br /> 當小數位數為 0 時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別屬性僅適用於 **integer**、**numeric** 和 **decimal** 類型。 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者嘗試在伺服器上建立資料表時，將屬性設定為任何其他資料類型之資料行上的 VARIANT_TRUE 時，會產生錯誤。<br /><br /> 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBPROP_COL_AUTOINCREMENT 和 DBPROP_COL_NullABLE 同時 VARIANT_TRUE，而且 DBPROP_COL_NullABLE 的*dwOption*不 DBPROPOPTIONS_REQUIRED 時，Native Client OLE DB 提供者會傳回 DB_S_ERRORSOCCURRED。 當 DBPROP_COL_AUTOINCREMENT 和 DBPROP_COL_NULLABLE 同時為 VARIANT_TRUE，而且 DBPROP_COL_NULLABLE 的 *dwOption* 等於 DBPROPOPTIONS_REQUIRED 時，會傳回 DB_E_ERRORSOCCURRED。 資料行會以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別屬性定義，而 DBPROP_COL_NULLABLE *dwStatus* 成員會設定為 DBPROPSTATUS_CONFLICTING。|  
|DBPROP_COL_DEFAULT|R/W：讀取/寫入<br /><br /> 預設值︰無<br /><br /> 描述：建立資料行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DEFAULT 條件約束。<br /><br /> 
  *vValue* DBPROP 成員可以是任何一種類型。 
  *vValue.vt* 成員應該指定一個與資料行資料類型相容的類型。 例如，對於定義為 DBTYPE_WSTR 的資料行而言，將 BSTR N/A 定義為預設值是相容符合。 在定義為 DBTYPE_R8 的資料行上定義相同的預設值時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]當 Native Client OLE DB 提供者嘗試在伺服器上建立資料表時，就會產生錯誤。|  
|DBPROP_COL_DESCRIPTION|R/W：讀取/寫入<br /><br /> 預設值︰無<br /><br /> 描述： DBPROP_COL_DESCRIPTION 的資料行屬性不是由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者所執行。<br /><br /> 當取用者嘗試寫入屬性值時，DBPROP 結構的 *dwStatus* 成員會傳回 DBPROPSTATUS_NOTSUPPORTED。<br /><br /> 設定屬性不會構成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者的嚴重錯誤。 如果其他所有參數值都有效，則會建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。|  
|DBPROP_COL_FIXEDLENGTH|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述：當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]取用者使用 DBCOLUMNDESC 的*wType*成員定義資料行的資料類型時，Native Client OLE DB 提供者會使用 DBPROP_COL_FIXEDLENGTH 來決定資料類型對應。 如需詳細資訊，請參閱[ITableDefinition 中的資料類型對應](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-itabledefinition.md)。|  
|DBPROP_COL_NULLABLE|R/W：讀取/寫入<br /><br /> 預設值︰無<br /><br /> 描述：建立資料表時，如果已[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]設定屬性，Native Client OLE DB 提供者會指出資料行是否應該接受 null 值。 未設定屬性時，資料行是否能夠接受 NULL 做為值取決於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ANSI_NULLS 預設資料庫選項。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者是與 ISO 相容的提供者。 已連接的工作階段會表現 ISO 行為。 如果取用者沒有設定 DBPROP_COL_NULLABLE，資料行接受 Null 值。|  
|DBPROP_COL_PRIMARYKEY|R/W：讀取/寫入<br /><br /> 預設值： VARIANT_FALSE 描述：當 VARIANT_TRUE 時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，Native Client OLE DB 提供者會建立具有 PRIMARY KEY 條件約束的資料行。<br /><br /> 定義為資料行屬性時，只有單一資料行可以決定條件約束。 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者嘗試建立[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表時，針對多個單一資料行設定屬性 VARIANT_TRUE 會傳回錯誤。<br /><br /> 注意：取用者可以使用 **IIndexDefinition::CreateIndex** 在兩個以上的資料行上建立 PRIMARY KEY 條件約束。<br /><br /> 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBPROP_COL_PRIMARYKEY 和 DBPROP_COL_UNIQUE 同時 VARIANT_TRUE，而且 DBPROP_COL_UNIQUE 的*dwOption*不 DBPROPOPTIONS_REQUIRED 時，Native Client OLE DB 提供者會傳回 DB_S_ERRORSOCCURRED。<br /><br /> 當 DBPROP_COL_PRIMARYKEY 和 DBPROP_COL_UNIQUE 同時為 VARIANT_TRUE，而且 DBPROP_COL_UNIQUE 的 *dwOption* 等於 DBPROPOPTIONS_REQUIRED 時，會傳回 DB_E_ERRORSOCCURRED。 資料行會以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別屬性定義，而 DBPROP_COL_PRIMARYKEY *dwStatus* 成員會設定為 DBPROPSTATUS_CONFLICTING。<br /><br /> 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBPROP_COL_PRIMARYKEY 和 DBPROP_COL_NullABLE 都 VARIANT_TRUE 時，Native Client OLE DB 提供者會傳回錯誤。<br /><br /> 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]取用者嘗試在無效[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料類型的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料行上建立 PRIMARY KEY 條件約束時，Native Client OLE DB 提供者會從傳回錯誤。 在使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型 **bit**、**text**、**ntext** 和 **image** 建立的資料行上，無法定義 PRIMARY KEY 條件約束。|  
|DBPROP_COL_UNIQUE|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE 描述：將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UNIQUE 條件約束套用到資料行。<br /><br /> 定義為資料行屬性時，僅會在單一資料行上套用條件約束。 取用者可以使用 **IIndexDefinition::CreateIndex**，在結合兩個或多個資料行的值上套用 UNIQUE 條件約束。<br /><br /> 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBPROP_COL_PRIMARYKEY 和 DBPROP_COL_UNIQUE 都是 VARIANT_TRUE 而且*dwOption*不 DBPROPOPTIONS_REQUIRED 時，Native Client OLE DB 提供者會傳回 DB_S_ERRORSOCCURRED。<br /><br /> 當 DBPROP_COL_PRIMARYKEY 和 DBPROP_COL_UNIQUE 同時為 VARIANT_TRUE，而且 *dwOption* 等於 DBPROPOPTIONS_REQUIRED 時，會傳回 DB_E_ERRORSOCCURRED。 資料行會以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別屬性定義，而 DBPROP_COL_PRIMARYKEY *dwStatus* 成員會設定為 DBPROPSTATUS_CONFLICTING。<br /><br /> 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBPROP_COL_NullABLE 和 DBPROP_COL_UNIQUE 都是 VARIANT_TRUE 而且*dwOption*不 DBPROPOPTIONS_REQUIRED 時，Native Client OLE DB 提供者會傳回 DB_S_ERRORSOCCURRED。<br /><br /> 當 DBPROP_COL_NULLABLE 和 DBPROP_COL_UNIQUE 同時為 VARIANT_TRUE，而且 *dwOption* 等於 DBPROPOPTIONS_REQUIRED 時，會傳回 DB_E_ERRORSOCCURRED。 資料行會以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別屬性定義，而 DBPROP_COL_NULLABLE *dwStatus* 成員會設定為 DBPROPSTATUS_CONFLICTING。<br /><br /> 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]取用者嘗試在無效[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料類型的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料行上建立 UNIQUE 條件約束時，Native Client OLE DB 提供者會從傳回錯誤。 在使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bit** 資料類型建立的資料行上，無法定義 UNIQUE 條件約束。|  
  
 當取用者呼叫**ITableDefinition：： CreateTable**時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會依照下列方式解讀資料表屬性。  
  
|屬性識別碼|描述|  
|-----------------|-----------------|  
|DBPROP_TBL_TEMPTABLE|R/W：讀取/寫入<br /><br /> 預設值： VARIANT_FALSE 描述：根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會建立由取用者命名的資料表。 當 VARIANT_TRUE 時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會產生取用者的臨時表名稱。 取用者會將 *CreateTable* 的 **pTableID** 參數設定為 NULL。 
  *ppTableID* 參數必須包含有效的指標。|  
  
 如果取用者要求在成功建立的資料表上開啟資料列集， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者會開啟資料指標支援的資料列集。 在傳遞的屬性集中可以指出任何資料列集屬性。  
  
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
  
  
