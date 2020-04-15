---
title: 建立 SQL Server 資料表 | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6f3d1ae29828e18cf98941666e7884e70115ba39
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301859"
---
# <a name="creating-sql-server-tables"></a>建立 SQL Server 資料表
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 OLE 資料庫提供程式公開**ITable 定義::createTable**函數,允許使用者[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]創建表。 消費者使用**CreateTable**創建名為消費者命名的永久表,以及具有本機用戶端 OLE[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料庫提供程式生成的唯一名稱的永久表或暫時表。  
  
 當消費者調用**ITable 定義::createTable**,如果DBPROP_TBL_TEMPTABLE屬性的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]值VARIANT_TRUE, 本機用戶端 OLE DB 提供程式將生成消費者的臨時表名。 取用者會將 **CreateTable** 方法的 *pTableID* 參數設定為 NULL。 具有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式生成名稱的暫存表不顯示在**TABLES**行集中,但可透過**IOpenRowset**介面存取。  
  
 當消費者在*pTableID*參數中的 uName 聯合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的*pwszName*成員中指定表名稱時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)],本機用戶端 OLE 資料庫提供程式將創建*uName*一個具有該名稱的表。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表的命名條件約束便會套用，而且資料表名稱可以表示永久資料表，或者本機或全域暫存資料表。 有關詳細資訊,請參閱[建立表](../../t-sql/statements/create-table-transact-sql.md)格 。 *ppTableID* 參數可以是 NULL。  
  
 本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 OLE 資料庫提供者可以生成永久表或暫存表的名稱。 當消費者將*pTableID*參數設定為 NULL 並將*ppTableID*設定以指向\*有效的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DBID 時,本機用戶端 OLE 資料庫提供者將傳回 DBID *uName*的*pwszName*成員中的表的產生名稱,該名稱由*ppTableID*的值指向 。 要建立臨時的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式命名表,消費者在*rgPropertySets*參數中引用的表屬性集中包括 OLE DB 表屬性DBPROP_TBL_TEMPTABLE。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式命名的暫時表是本地的。  
  
 如果 **pTableID** 參數的 *eKind* 成員不包含 DBKIND_NAME，*CreateTable* 會傳回 DB_E_BADTABLEID。  
  
## <a name="dbcolumndesc-usage"></a>DBCOLUMNDESC 用法  
 取用者可以使用 *pwszTypeName* 成員或 *wType* 成員來指出資料行資料類型。 如果消費者在*pwszTypeName*中指定數據類型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)],則本機用戶端 OLE 資料庫提供程式將忽略*wType*的值。  
  
 如果使用 *pwszTypeName* 成員，取用者會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型名稱指定資料類型。 有效的資料類型名稱是在 PROVIDER_TYPES 結構描述資料列集之 TYPE_NAME 資料行中傳回的資料類型名稱。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供者在*wType*成員中識別 OLE DB 枚舉 DBTYPE 值的子集。 如需詳細資訊，請參閱 [ITableDefinition 中的資料類型對應](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-itabledefinition.md)。  
  
> [!NOTE]  
>  如果取用者將 *pTypeInfo* 或 *pclsid* 成員設定為指定資料行資料類型，**CreateTable** 會傳回 DB_E_BADTYPE。  
  
 取用者會在 DBCOLUMNDESC *dbcid* 成員之 *uName* 聯集的 *pwszName* 成員中，指定資料行名稱。 資料行名稱會指定為 Unicode 字元字串。 *dbcid* 的 *eKind* 成員必須是 DBKIND_NAME。 如果 *eKind* 無效、*pwszName* 為 NULL，或者 *pwszName* 的值不是有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別碼，**CreateTable** 會傳回 DB_E_BADCOLUMNID。  
  
 在針對資料表定義的所有資料行上都可以使用所有資料行屬性。 如果屬性值的設定發生衝突，**CreateTable** 可能會傳回 DB_S_ERRORSOCCURRED 或 DB_E_ERRORSOCCURRED。 當無效的資料行屬性設定造成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表建立失敗時，**CreateTable** 會傳回錯誤。  
  
 DBCOLUMNDESC 中的資料行屬性解譯如下。  
  
|屬性識別碼|描述|  
|-----------------|-----------------|  
|DBPROP_COL_AUTOINCREMENT|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE 描述：在建立的資料行上設定識別屬性。 對於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，識別屬性適用於資料表內的單一資料行。 將屬性設置為多個列的VARIANT_TRUE,當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式嘗試在伺服器上創建表時,將生成錯誤。<br /><br /> 當小數位數為 0 時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別屬性僅適用於 **integer**、**numeric** 和 **decimal** 類型。 將屬性設置為任何其他資料類型的列上的VARIANT_TRUE在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式嘗試在伺服器上創建表時生成錯誤。<br /><br /> 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DBPROP_COL_AUTOINCREMENT和DBPROP_COL_NULLABLE都VARIANT_TRUE,並且DBPROP_COL_NULLABLE的*dwOption*不DBPROPOPTIONS_REQUIRED時,本機用戶端 OLE 資料庫提供程式將返回DB_S_ERRORSOCCURRED。 當 DBPROP_COL_AUTOINCREMENT 和 DBPROP_COL_NULLABLE 同時為 VARIANT_TRUE，而且 DBPROP_COL_NULLABLE 的 *dwOption* 等於 DBPROPOPTIONS_REQUIRED 時，會傳回 DB_E_ERRORSOCCURRED。 資料行會以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別屬性定義，而 DBPROP_COL_NULLABLE *dwStatus* 成員會設定為 DBPROPSTATUS_CONFLICTING。|  
|DBPROP_COL_DEFAULT|R/W：讀取/寫入<br /><br /> 預設值：無<br /><br /> 描述：建立資料行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DEFAULT 條件約束。<br /><br /> *vValue* DBPROP 成員可以是任何一種類型。 *vValue.vt* 成員應該指定一個與資料行資料類型相容的類型。 例如，對於定義為 DBTYPE_WSTR 的資料行而言，將 BSTR N/A 定義為預設值是相容符合。 在定義為DBTYPE_R8的列上定義相同的預設值,當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式嘗試在伺服器上創建表時,將生成錯誤。|  
|DBPROP_COL_DESCRIPTION|R/W：讀取/寫入<br /><br /> 預設值：無<br /><br /> 說明: DBPROP_COL_DESCRIPTION欄屬性不是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]由 本機用戶端 OLE DB 提供程式實現的。<br /><br /> 當取用者嘗試寫入屬性值時，DBPROP 結構的 *dwStatus* 成員會傳回 DBPROPSTATUS_NOTSUPPORTED。<br /><br /> 設置該屬性並不構成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式的致命錯誤。 如果其他所有參數值都有效，則會建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。|  
|DBPROP_COL_FIXEDLENGTH|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 說明:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式使用DBPROP_COL_FIXEDLENGTH,當消費者使用 DBCOLUMNDESC 的*wType*成員定義列的數據類型時,使用DBPROP_COL_FIXEDLENGTH來確定數據類型映射。 如需詳細資訊，請參閱 [ITableDefinition 中的資料類型對應](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-itabledefinition.md)。|  
|DBPROP_COL_NULLABLE|R/W：讀取/寫入<br /><br /> 預設值：無<br /><br /> 說明:建立表時,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式指示如果設定該屬性,列是否應接受空值。 未設定屬性時，資料行是否能夠接受 NULL 做為值取決於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ANSI_NULLS 預設資料庫選項。<br /><br /> 本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 OLE 資料庫提供程式是符合 ISO 的提供程式。 已連接的工作階段會表現 ISO 行為。 如果取用者沒有設定 DBPROP_COL_NULLABLE，資料行接受 Null 值。|  
|DBPROP_COL_PRIMARYKEY|R/W：讀取/寫入<br /><br /> 預設值:VARIANT_FALSE說明:VARIANT_TRUE時,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式使用"主要密鑰"約束創建列。<br /><br /> 定義為資料行屬性時，只有單一資料行可以決定條件約束。 為多個列設定屬性VARIANT_TRUE返回[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE DB 提供程式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]嘗試創建表時的錯誤。<br /><br /> 注意：取用者可以使用 **IIndexDefinition::CreateIndex** 在兩個以上的資料行上建立 PRIMARY KEY 條件約束。<br /><br /> 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]VARIANT_TRUEDBPROP_COL_PRIMARYKEY和DBPROP_COL_UNIQUE且 DBPROP_COL_UNIQUE的*dwOption*不DBPROPOPTIONS_REQUIRED時,本機用戶端 OLE 資料庫提供程式將返回DB_S_ERRORSOCCURRED。<br /><br /> 當 DBPROP_COL_PRIMARYKEY 和 DBPROP_COL_UNIQUE 同時為 VARIANT_TRUE，而且 DBPROP_COL_UNIQUE 的 *dwOption* 等於 DBPROPOPTIONS_REQUIRED 時，會傳回 DB_E_ERRORSOCCURRED。 資料行會以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別屬性定義，而 DBPROP_COL_PRIMARYKEY *dwStatus* 成員會設定為 DBPROPSTATUS_CONFLICTING。<br /><br /> 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DBPROP_COL_PRIMARYKEY和DBPROP_COL_NULLABLE都VARIANT_TRUE時,本機用戶端 OLE 資料庫提供程式將返回錯誤。<br /><br /> 本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 OLE 資料庫提供程式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用者 嘗試在無效 資料類型列上創建"主要密鑰"約束時的錯誤。 在使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型 **bit**、**text**、**ntext** 和 **image** 建立的資料行上，無法定義 PRIMARY KEY 條件約束。|  
|DBPROP_COL_UNIQUE|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE 描述：將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UNIQUE 條件約束套用到資料行。<br /><br /> 定義為資料行屬性時，僅會在單一資料行上套用條件約束。 取用者可以使用 **IIndexDefinition::CreateIndex**，在結合兩個或多個資料行的值上套用 UNIQUE 條件約束。<br /><br /> 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DBPROP_COL_PRIMARYKEY和DBPROP_COL_UNIQUE都VARIANT_TRUE,*並且不DBPROPOPTIONS_REQUIRED dwOption*時,本機用戶端 OLE 資料庫提供程式將返回DB_S_ERRORSOCCURRED。<br /><br /> 當 DBPROP_COL_PRIMARYKEY 和 DBPROP_COL_UNIQUE 同時為 VARIANT_TRUE，而且 *dwOption* 等於 DBPROPOPTIONS_REQUIRED 時，會傳回 DB_E_ERRORSOCCURRED。 資料行會以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別屬性定義，而 DBPROP_COL_PRIMARYKEY *dwStatus* 成員會設定為 DBPROPSTATUS_CONFLICTING。<br /><br /> 當[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DBPROP_COL_NULLABLE和DBPROP_COL_UNIQUE都VARIANT_TRUE並且不DBPROPOPTIONS_REQUIRED *dwOption*時,本機用戶端 OLE 資料庫提供程式將返回DB_S_ERRORSOCCURRED。<br /><br /> 當 DBPROP_COL_NULLABLE 和 DBPROP_COL_UNIQUE 同時為 VARIANT_TRUE，而且 *dwOption* 等於 DBPROPOPTIONS_REQUIRED 時，會傳回 DB_E_ERRORSOCCURRED。 資料行會以 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 識別屬性定義，而 DBPROP_COL_NULLABLE *dwStatus* 成員會設定為 DBPROPSTATUS_CONFLICTING。<br /><br /> 本機[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端 OLE 資料庫提供程式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用者嘗試在無效 資料類型列上創建 UNIQUE 約束時的錯誤。 在使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **bit** 資料類型建立的資料行上，無法定義 UNIQUE 條件約束。|  
  
 當消費者調用**ITable 定義::createTable**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時,本機用戶端 OLE 資料庫提供程式將表屬性解釋如下。  
  
|屬性識別碼|描述|  
|-----------------|-----------------|  
|DBPROP_TBL_TEMPTABLE|R/W：讀取/寫入<br /><br /> 預設值:VARIANT_FALSE說明:預設情況下,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式創建由消費者命名的表。 VARIANT_TRUE時,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式會為消費者生成臨時表名稱。 取用者會將 **CreateTable** 的 *pTableID* 參數設定為 NULL。 *ppTableID* 參數必須包含有效的指標。|  
  
 如果使用者請求在成功建立的表上打開行集,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本機用戶端 OLE 資料庫提供程式將打開一個支援游標的行集。 在傳遞的屬性集中可以指出任何資料列集屬性。  
  
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
  
  
