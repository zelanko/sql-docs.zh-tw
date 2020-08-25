---
description: Microsoft OLE DB Provider for ODBC 總覽
title: Microsoft OLE DB Provider for ODBC |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB provider for ODBC [ADO]
- providers [ADO], OLE DB provider for ODBC
ms.assetid: 2dc0372d-e74d-4d0f-9c8c-04e5a168c148
author: rothja
ms.author: jroth
ms.openlocfilehash: 2dcd280098a5ca4075f424f12b0abdfede6b7653
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806646"
---
# <a name="microsoft-ole-db-provider-for-odbc-overview"></a>Microsoft OLE DB Provider for ODBC 總覽
對於 ADO 或 RDS 程式設計師而言，理想的世界就是每個資料來源都會公開 OLE DB 介面，因此 ADO 可以直接呼叫資料來源。 雖然越來越多的資料庫供應商正在執行 OLE DB 介面，但有些資料來源尚未以這種方式公開。 不過，目前使用中的大部分 DBMS 系統都可以透過 ODBC 來存取。

 ODBC 驅動程式適用于現今使用的每個主要 DBMS，包括 Microsoft SQL Server、Microsoft Access (Microsoft Jet database engine) 和 Microsoft FoxPro，以及非 Microsoft 資料庫產品（例如 Oracle）。

 但是，Microsoft ODBC 提供者允許 ADO 連接到任何 ODBC 資料來源。 提供者是無限制執行緒和 Unicode 啟用。

 雖然不同的 DBMS 引擎提供不同類型的交易支援，但是提供者支援交易。 例如，Microsoft Access 支援最多五個層級的嵌套交易。

 這是 ADO 的預設提供者，而且支援所有提供者相依的 ADO 屬性和方法。

## <a name="connection-string-parameters"></a>連接字串參數
 若要連接到這個提供者，請將[ConnectionString](../../reference/ado-api/connectionstring-property-ado.md)屬性的**provider =** 引數設定為：

```
MSDASQL
```

 讀取 [Provider](../../reference/ado-api/provider-property-ado.md) 屬性也會傳回這個字串。

## <a name="typical-connection-string"></a>一般連接字串
 此提供者的一般連接字串為：

```
"Provider=MSDASQL;DSN=dsnName;UID=MyUserID;PWD=MyPassword;"
```

 此字串包含下列關鍵字：

|關鍵字|描述|
|-------------|-----------------|
|**提供者**|指定 ODBC 的 OLE DB 提供者。|
|**DSN**|指定資料來源名稱。|
|**UID**|指定使用者名稱。|
|**PWD**|指定使用者密碼。|
|**URL**|指定在 Web 資料夾中發佈之檔案或目錄的 URL。|

 因為這是 ADO 的預設提供者，所以如果您省略連接字串中的 **provider =** 參數，ADO 將會嘗試建立此提供者的連接。

> [!NOTE]
>  如果您要連接到支援 Windows 驗證的資料來源提供者，您應該在連接字串中指定 **Trusted_Connection = yes** 或 **整合式安全性 = SSPI** ，而不是使用者識別碼和密碼資訊。

 除了 ADO 定義的連接參數之外，提供者不支援任何特定的連接參數。 但是，提供者會將任何非 ADO 連接參數傳遞至 ODBC 驅動程式管理員。

 因為您可以省略 **Provider** 參數，所以您可以撰寫與相同資料來源的 ODBC 連接字串相同的 ADO 連接字串。 使用相同的參數名稱 (**DRIVER =**、 **DATABASE =**、 **DSN =** 等) 、值和語法，如同撰寫 ODBC 連接字串時所使用的一樣。 您可以使用或不使用預先定義的資料來源名稱 (DSN) 或 FileDSN 進行連接。

## <a name="syntax-with-a-dsn-or-filedsn"></a>具有 DSN 或 FileDSN 的語法：

```
"[Provider=MSDASQL;] { DSN=name | FileDSN=filename } ;
[DATABASE=database;] UID=user; PWD=password"
```

## <a name="syntax-without-a-dsn-dsn-less-connection"></a>沒有 DSN 的語法 (不使用 DSN 的連接) ：

```
"[Provider=MSDASQL;] DRIVER=driver; SERVER=server;
DATABASE=database; UID=MyUserID; PWD=MyPassword"
```

## <a name="remarks"></a>備註
 如果您使用 **DSN** 或 **FileDSN**，則必須透過 Windows 主控台中的「ODBC 資料來源管理員」定義。 在 Microsoft Windows 2000 中，ODBC 系統管理員位於 [系統管理工具] 下。 在舊版的 Windows 中，ODBC 管理員圖示的名稱是 **32 位 odbc** 或單純是 **odbc**。

 除了設定 **DSN**之外，您還可以指定 ODBC 驅動程式 (**driver =**) ，例如 "SQL Server;" 伺服器名稱 (**server =**) ;和資料庫名稱 (**database =**) 。

 您也可以指定使用者帳戶名稱 (**UID =**) ，以及使用者帳戶的密碼 (**PWD =**) 在 ODBC 特定參數或標準 ADO 定義的 *使用者* 和 *密碼* 參數中。

 雖然**dsn**定義已經*指定資料庫，* 但除了**dsn**之外，您還可以指定*資料庫*參數來連接至不同的資料庫。 當您使用**DSN***時，最好一律包含**資料庫*參數。 如果有其他使用者變更了自您上次檢查 **DSN** 定義之後的預設資料庫參數，這將可確保您連接到正確的資料庫。

## <a name="provider-specific-connection-properties"></a>提供者特定的連接屬性
 ODBC 的 OLE DB provider 會將數個屬性加入至**Connection**物件的[properties](../../reference/ado-api/properties-collection-ado.md)集合中。 下表列出這些屬性，這些屬性具有對應的 OLE DB 屬性名稱（以括弧括住）。

|屬性名稱|描述|
|-------------------|-----------------|
| (KAGPROP_ACCESSIBLEPROCEDURES 的可存取程式) |指出使用者是否有預存程式的存取權。|
|可存取的資料表 (KAGPROP_ACCESSIBLETABLES) |指出使用者是否有許可權對資料庫資料表執行 SELECT 語句。|
|現用語句 (KAGPROP_ACTIVESTATEMENTS) |指出 ODBC 驅動程式可在連接上支援的控制碼數目。|
|驅動程式名稱 (KAGPROP_DRIVERNAME) |指出 ODBC 驅動程式的檔案名。|
|驅動程式 ODBC 版本 (KAGPROP_DRIVERODBCVER) |指出此驅動程式支援的 ODBC 版本。|
|檔案使用 (KAGPROP_FILEUSAGE) |指出驅動程式如何處理資料來源中的檔案;做為資料表或目錄。|
|Like Escape 子句 (KAGPROP_LIKEESCAPECLAUSE) |指出驅動程式是否支援在 WHERE 子句的 LIKE 述詞中，針對 percent 字元 (% ) 和底線字元 (_) 定義和使用 escape 字元。|
|[群組依據] 中的資料行最大值 (KAGPROP_MAXCOLUMNSINGROUPBY) |指出可在 SELECT 語句的 GROUP BY 子句中列出的資料行數目上限。|
|索引中的最大資料行 (KAGPROP_MAXCOLUMNSININDEX) |指出可包含在索引中的最大資料行數目。|
|Order By (KAGPROP_MAXCOLUMNSINORDERBY) 的最大資料行|指出可在 SELECT 語句的 ORDER BY 子句中列出的資料行數目上限。|
|Select (KAGPROP_MAXCOLUMNSINSELECT 中的最大資料行) |表示可以在 SELECT 語句的 SELECT 部分中列出的資料行數目上限。|
|資料表中的資料行數上限 (KAGPROP_MAXCOLUMNSINTABLE) |指出資料表中允許的資料行數目上限。|
|數值函式 (KAGPROP_NUMERICFUNCTIONS) |指出 ODBC 驅動程式所支援的數值函數。 如需函式名稱和此位元遮罩中所用關聯值的清單，請參閱 ODBC 檔中的 [附錄 E：](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)純量函數。|
|外部聯結功能 (KAGPROP_OJCAPABILITY) |表示提供者所支援的外部聯結類型。|
|外部聯結 (KAGPROP_OUTERJOINS) |指出提供者是否支援外部聯結。|
| (KAGPROP_SPECIALCHARACTERS) 的特殊字元|指出哪些字元對 ODBC 驅動程式具有特殊意義。|
|預存程式 (KAGPROP_PROCEDURES) |指出預存程式是否可用於此 ODBC 驅動程式。|
|字串函式 (KAGPROP_STRINGFUNCTIONS) |指出 ODBC 驅動程式所支援的字串函數。 如需函式名稱和此位元遮罩中所用關聯值的清單，請參閱 ODBC 檔中的 [附錄 E：](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)純量函數。|
|系統函式 (KAGPROP_SYSTEMFUNCTIONS) |指出 ODBC 驅動程式支援哪些系統函數。 如需函式名稱和此位元遮罩中所用關聯值的清單，請參閱 ODBC 檔中的 [附錄 E：](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)純量函數。|
|時間/日期函數 (KAGPROP_TIMEDATEFUNCTIONS) |指出 ODBC 驅動程式所支援的時間和日期函數。 如需函式名稱和此位元遮罩中所用關聯值的清單，請參閱 ODBC 檔中的 [附錄 E：](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)純量函數。|
| (KAGPROP_ODBCSQLCONFORMANCE) 的 SQL 文法支援|指出 ODBC 驅動程式支援的 SQL 文法。|

## <a name="provider-specific-recordset-and-command-properties"></a>提供者特定的記錄集和命令屬性
 ODBC 的 OLE DB provider 會將數個屬性加入至**記錄集**和**命令**物件的**properties**集合中。 下表列出這些屬性，這些屬性具有對應的 OLE DB 屬性名稱（以括弧括住）。

|屬性名稱|描述|
|-------------------|-----------------|
|以查詢為基礎的更新/刪除/插入 (KAGPROP_QUERYBASEDUPDATES) |指出是否可以使用 SQL 查詢來執行更新、刪除和插入。|
|ODBC 並行類型 (KAGPROP_CONCURRENCY) |指出方法，此方法可用來減少兩位使用者同時嘗試從資料來源存取相同資料所造成的潛在問題。|
|順向資料指標上的 BLOB 存取範圍 (KAGPROP_BLOBSONFOCURSOR) |指出使用順向資料指標時，是否可以存取 BLOB **欄位** 。|
|在 QBU WHERE 子句 (KAGPROP_INCLUDENONEXACT 中包含 SQL_FLOAT、SQL_DOUBLE 和 SQL_REAL) |指出 SQL_FLOAT、SQL_DOUBLE 和 SQL_REAL 值是否可以包含在 QBU WHERE 子句中。|
|插入 (KAGPROP_POSITIONONNEWROW 後最後一個資料列上的位置) |表示在新記錄插入資料表之後，資料表中的最後一個資料列會是目前的資料列。|
|IRowsetChangeExtInfo (KAGPROP_IROWSETCHANGEEXTINFO) |指出 **IRowsetChange** 介面是否提供延伸的資訊支援。|
|ODBC 資料指標類型 (KAGPROP_CURSOR) |指出 **記錄集**所使用的資料指標類型。|
|產生可封送處理 (KAGPROP_MARSHALLABLE 的資料列集) |指出 ODBC 驅動程式會產生可封送處理的記錄集|

## <a name="command-text"></a>命令文字
 您如何使用 [命令](../../reference/ado-api/command-object-ado.md) 物件主要取決於資料來源，以及它將接受的查詢或命令語句類型。

 ODBC 提供用來呼叫預存程式的特定語法。 對於**Command**物件的[Commandtext](../../reference/ado-api/commandtext-property-ado.md)屬性，[連接](../../reference/ado-api/connection-object-ado.md)物件上**Execute**方法的*Commandtext*引數，或[記錄集](../../reference/ado-api/recordset-object-ado.md)物件上**Open**方法的*Source*引數，會以下列語法傳入字串：

```
"{ [ ? = ] call procedure [ ( ? [, ? [ , ... ]] ) ] }"
```

 每個 **？** 參考 [Parameters](../../reference/ado-api/parameters-collection-ado.md) 集合中的物件。 第一個 **？**  (0) 的參考 **參數** ，下一步是 **什麼？** 參考 **參數** (1) 等等。

 參數參考是選擇性的，且取決於預存程式的結構。 如果您想要呼叫未定義任何參數的預存程式，則您的字串看起來會如下所示：

```
"{ call procedure }"
```

 如果您有兩個查詢參數，您的字串會類似下列內容：

```
"{ call procedure ( ?, ? ) }"
```

 如果預存程式將傳回值，則會將傳回值視為另一個參數。 如果您沒有查詢參數，但您有傳回值，則字串會類似下列內容：

```
"{ ? = call procedure }"
```

 最後，如果您有傳回值和兩個查詢參數，則您的字串會類似下列內容：

```
"{ ? = call procedure ( ?, ? ) }"
```

## <a name="recordset-behavior"></a>記錄集行為
 下表列出使用此提供者開啟之 **記錄集** 物件上可用的標準 ADO 方法和屬性。

 如需提供者設定的**記錄集**行為詳細資訊，請執行[支援](../../reference/ado-api/supports-method.md)的方法，並列舉**記錄集**的**屬性**集合，以判斷是否存在提供者特定的動態屬性。

 標準 ADO **記錄集** 屬性的可用性：

|屬性|ForwardOnly|動態|索引鍵集|靜態|
|--------------|-----------------|-------------|------------|------------|
|[AbsolutePage](../../reference/ado-api/absolutepage-property-ado.md)|無法使用|無法使用|讀取/寫入|讀取/寫入|
|[AbsolutePosition](../../reference/ado-api/absoluteposition-property-ado.md)|無法使用|無法使用|讀取/寫入|讀取/寫入|
|[ActiveConnection](../../reference/ado-api/activeconnection-property-ado.md)|讀取/寫入|讀取/寫入|讀取/寫入|讀取/寫入|
|[轉爐](../../reference/ado-api/bof-eof-properties-ado.md)|唯讀|唯讀|唯讀|唯讀|
|[書籤](../../reference/ado-api/bookmark-property-ado.md)|無法使用|無法使用|讀取/寫入|讀取/寫入|
|[CacheSize](../../reference/ado-api/cachesize-property-ado.md)|讀取/寫入|讀取/寫入|讀取/寫入|讀取/寫入|
|[CursorLocation](../../reference/ado-api/cursorlocation-property-ado.md)|讀取/寫入|讀取/寫入|讀取/寫入|讀取/寫入|
|[CursorType](../../reference/ado-api/cursortype-property-ado.md)|讀取/寫入|讀取/寫入|讀取/寫入|讀取/寫入|
|[EditMode](../../reference/ado-api/editmode-property.md)|唯讀|唯讀|唯讀|唯讀|
|[Filter](../../reference/ado-api/filter-property.md)|讀取/寫入|讀取/寫入|讀取/寫入|讀取/寫入|
|[LockType](../../reference/ado-api/locktype-property-ado.md)|讀取/寫入|讀取/寫入|讀取/寫入|讀取/寫入|
|[MarshalOptions](../../reference/ado-api/marshaloptions-property-ado.md)|讀取/寫入|讀取/寫入|讀取/寫入|讀取/寫入|
|[MaxRecords](../../reference/ado-api/maxrecords-property-ado.md)|讀取/寫入|讀取/寫入|讀取/寫入|讀取/寫入|
|[PageCount](../../reference/ado-api/pagecount-property-ado.md)|讀取/寫入|無法使用|唯讀|唯讀|
|[PageSize](../../reference/ado-api/pagesize-property-ado.md)|讀取/寫入|讀取/寫入|讀取/寫入|讀取/寫入|
|[RecordCount](../../reference/ado-api/recordcount-property-ado.md)|讀取/寫入|無法使用|唯讀|唯讀|
|[Source](../../reference/ado-api/source-property-ado-recordset.md)|讀取/寫入|讀取/寫入|讀取/寫入|讀取/寫入|
|[State](../../reference/ado-api/state-property-ado.md)|唯讀|唯讀|唯讀|唯讀|
|[狀態](../../reference/ado-api/status-property-ado-recordset.md)|唯讀|唯讀|唯讀|唯讀|

 [AbsolutePosition](../../reference/ado-api/absoluteposition-property-ado.md)和[AbsolutePage](../../reference/ado-api/absolutepage-property-ado.md)屬性只有在使用 ADO 搭配 MICROSOFT OLE DB Provider for ODBC 的1.0 版時，才是寫入的。

 標準 ADO **記錄集** 方法的可用性：

|方法|ForwardOnly|動態|索引鍵集|靜態|
|------------|-----------------|-------------|------------|------------|
|[AddNew](../../reference/ado-api/addnew-method-ado.md)|是|是|是|是|
|[取消](../../reference/ado-api/cancel-method-ado.md)|是|是|是|是|
|[CancelBatch](../../reference/ado-api/cancelbatch-method-ado.md)|是|是|是|是|
|[CancelUpdate](../../reference/ado-api/cancelupdate-method-ado.md)|是|是|是|是|
|[複製](../../reference/ado-api/clone-method-ado.md)|否|否|是|是|
|[關閉](../../reference/ado-api/close-method-ado.md)|是|是|是|是|
|[刪除](../../reference/ado-api/delete-method-ado-recordset.md)|是|是|是|是|
|[GetRows](../../reference/ado-api/getrows-method-ado.md)|是|是|是|是|
|[移動](../../reference/ado-api/move-method-ado.md)|是|是|是|是|
|[MoveFirst](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|是|是|是|是|
|[MoveLast](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|否|是|是|是|
|[MoveNext](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|是|是|是|是|
|[MovePrevious](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|否|是|是|是|
|[NextRecordset](../../reference/ado-api/nextrecordset-method-ado.md)*|是|是|是|是|
|[開啟](../../reference/ado-api/open-method-ado-recordset.md)|是|是|是|是|
|[重新](../../reference/ado-api/requery-method.md)|是|是|是|是|
|[重新同步處理](../../reference/ado-api/resync-method.md)|否|否|是|是|
|[支援](../../reference/ado-api/supports-method.md)|是|是|是|是|
|[更新](../../reference/ado-api/update-method.md)|是|是|是|是|
|[UpdateBatch](../../reference/ado-api/updatebatch-method.md)|是|是|是|是|

 * 不支援 Microsoft Access 資料庫。

## <a name="dynamic-properties"></a>動態屬性
 Microsoft OLE DB Provider for ODBC 會將數個動態屬性插入未開啟之[連接](../../reference/ado-api/connection-object-ado.md)、[記錄集](../../reference/ado-api/recordset-object-ado.md)和[命令](../../reference/ado-api/command-object-ado.md)物件的**properties**集合中。

 下表是每個動態屬性之 ADO 和 OLE DB 名稱的交叉索引。 OLE DB 程式設計人員參考是依「描述」一詞來參考 ADO 屬性名稱。 您可以在 OLE DB 程式設計人員參考中找到這些屬性的詳細資訊。 在索引中搜尋 OLE DB 的屬性名稱，或參閱 [附錄 C： OLE DB 屬性](/previous-versions/windows/desktop/ms723130(v=vs.85))。

## <a name="connection-dynamic-properties"></a>連接動態屬性
 下列屬性會加入至 **連接** 物件的 **屬性** 集合。

|ADO 屬性名稱|OLE DB 屬性名稱|
|-----------------------|--------------------------|
|Active Sessions|DBPROP_ACTIVESESSIONS|
|Asynchable 中止|DBPROP_ASYNCTXNABORT|
|Asynchable 認可|DBPROP_ASYNCTNXCOMMIT|
|自動認可隔離等級|DBPROP_SESS_AUTOCOMMITISOLEVELS|
|目錄位置|DBPROP_CATALOGLOCATION|
|目錄詞彙|DBPROP_CATALOGTERM|
|資料行定義|DBPROP_COLUMNDEFINITION|
|連接逾時|DBPROP_INIT_TIMEOUT|
|目前的目錄|DBPROP_CURRENTCATALOG|
|資料來源|DBPROP_INIT_DATASOURCE|
|資料來源名稱|DBPROP_DATASOURCENAME|
|資料來源物件執行緒模型|DBPROP_DSOTHREADMODEL|
|DBMS 名稱|DBPROP_DBMSNAME|
|DBMS 版本|DBPROP_DBMSVER|
|擴充屬性|DBPROP_INIT_PROVIDERSTRING|
|依支援分組|DBPROP_GROUPBY|
|異質資料表支援|DBPROP_HETEROGENEOUSTABLES|
|識別碼區分大小寫|DBPROP_IDENTIFIERCASE|
|初始目錄|DBPROP_INIT_CATALOG|
|隔離等級|DBPROP_SUPPORTEDTXNISOLEVELS|
|隔離保留|DBPROP_SUPPORTEDTXNISORETAIN|
|地區設定識別碼|DBPROP_INIT_LCID|
|Location|DBPROP_INIT_LOCATION|
|索引大小上限|DBPROP_MAXINDEXSIZE|
|最大資料列大小|DBPROP_MAXROWSIZE|
|最大資料列大小包括 BLOB|DBPROP_MAXROWSIZEINCLUDESBLOB|
|SELECT 中的資料表上限|DBPROP_MAXTABLESINSELECT|
|[模式]|DBPROP_INIT_MODE|
|多個參數集|DBPROP_MULTIPLEPARAMSETS|
|多個結果|DBPROP_MULTIPLERESULTS|
|多個儲存物件|DBPROP_MULTIPLESTORAGEOBJECTS|
|多資料表更新|DBPROP_MULTITABLEUPDATE|
|Null 定序順序|DBPROP_NullCOLLATION|
|Null 串連行為|DBPROP_CONCATNULLBEHAVIOR|
|OLE DB 服務|DBPROP_INIT_OLEDBSERVICES|
|OLE DB 版本|DBPROP_PROVIDEROLEDBVER|
|OLE 物件支援|DBPROP_OLEOBJECTS|
|開啟資料列集支援|DBPROP_OPENROWSETSUPPORT|
|選取清單中的 ORDER BY 資料行|DBPROP_ORDERBYCOLUMNSINSELECT|
|輸出參數可用性|DBPROP_OUTPUTPARAMETERAVAILABILITY|
|密碼|DBPROP_AUTH_PASSWORD|
|以 Ref 存取子傳遞|DBPROP_BYREFACCESSORS|
|保存安全性資訊|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|
|持續性識別碼類型|DBPROP_PERSISTENTIDTYPE|
|準備中止行為|DBPROP_PREPAREABORTBEHAVIOR|
|準備認可行為|DBPROP_PREPARECOMMITBEHAVIOR|
|程式期限|DBPROP_PROCEDURETERM|
|Prompt|DBPROP_INIT_PROMPT|
|提供者易記名稱|DBPROP_PROVIDERFRIENDLYNAME|
|Provider Name|DBPROP_PROVIDERFILENAME|
|提供者版本|DBPROP_PROVIDERVER|
|唯讀資料來源|DBPROP_DATASOURCEREADONLY|
|命令的資料列集轉換|DBPROP_ROWSETCONVERSIONSONCOMMAND|
|架構詞彙|DBPROP_SCHEMATERM|
|架構使用方式|DBPROP_SCHEMAUSAGE|
|SQL 支援|DBPROP_SQLSUPPORT|
|結構化儲存體|DBPROP_STRUCTUREDSTORAGE|
|子查詢支援|DBPROP_SUBQUERIES|
|資料表詞彙|DBPROP_TABLETERM|
|交易 DDL|DBPROP_SUPPORTEDTXNDDL|
|使用者識別碼|DBPROP_AUTH_USERID|
|使用者名稱|DBPROP_USERNAME|
|視窗控制代碼|DBPROP_INIT_HWND|

## <a name="recordset-dynamic-properties"></a>記錄集動態屬性
 下列屬性會加入至 **記錄集** 物件的 **屬性** 集合。

|ADO 屬性名稱|OLE DB 屬性名稱|
|-----------------------|--------------------------|
|存取順序|DBPROP_ACCESSORDER|
|封鎖儲存物件|DBPROP_BLOCKINGSTORAGEOBJECTS|
|書簽類型|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|變更插入的資料列|DBPROP_CHANGEINSERTEDROWS|
|資料行許可權|DBPROP_COLUMNRESTRICT|
|資料行集通知|DBPROP_NOTIFYCOLUMNSET|
|延遲儲存物件更新|DBPROP_DELAYSTORAGEOBJECTS|
|向後提取|DBPROP_CANFETCHBACKWARDS|
|保留資料列|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|Immobile 資料列|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsetLocate|
|IRowsetResynch||
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|常值書簽|DBPROP_LITERALBOOKMARKS|
|常值資料列識別|DBPROP_LITERALIDENTITY|
|開啟的資料列數上限|DBPROP_MAXOPENROWS|
|暫止的資料列數上限|DBPROP_MAXPENDINGROWS|
|最大資料列數|DBPROP_MAXROWS|
|通知細微性|DBPROP_NOTIFICATIONGRANULARITY|
|通知階段|DBPROP_NOTIFICATIONPHASES|
|物件交易|DBPROP_TRANSACTEDOBJECT|
|可見的變更|DBPROP_OWNUPDATEDELETE|
|擁有可見的插入|DBPROP_OWNINSERT|
|中止時保留|DBPROP_ABORTPRESERVE|
|在認可時保留|DBPROP_COMMITPRESERVE|
|快速重新開機|DBPROP_QUICKRESTART|
|重新進入事件|DBPROP_REENTRANTEVENTS|
|移除刪除的資料列|DBPROP_REMOVEDELETED|
|報告多項變更|DBPROP_REPORTMULTIPLECHANGES|
|傳回暫止的插入|DBPROP_RETURNPENDINGINSERTS|
|資料列刪除通知|DBPROP_NOTIFYROWDELETE|
|Row First 變更通知|DBPROP_NOTIFYROWFIRSTCHANGE|
|資料列插入通知|DBPROP_NOTIFYROWINSERT|
|資料列許可權|DBPROP_ROWRESTRICT|
|資料列重新同步通知|DBPROP_NOTIFYROWRESYNCH|
|資料列執行緒模型|DBPROP_ROWTHREADMODEL|
|資料列復原變更通知|DBPROP_NOTIFYROWUNDOCHANGE|
|資料列恢復刪除通知|DBPROP_NOTIFYROWUNDODELETE|
|資料列復原插入通知|DBPROP_NOTIFYROWUNDOINSERT|
|資料列更新通知|DBPROP_NOTIFYROWUPDATE|
|資料列集提取位置變更通知|DBPROP_NOTIFYROWSETFETCHPOSISIONCHANGE|
|資料列集發行通知|DBPROP_NOTIFYROWSETRELEASE|
|向後滾動|DBPROP_CANSCROLLBACKWARDS|
|略過已刪除的書簽|DBPROP_BOOKMARKSKIPPED|
|強式資料列識別|DBPROP_STRONGITDENTITY|
|唯一資料列|DBPROP_UNIQUEROWS|
|更新|DBPROP_UPDATABILITY|
|使用書簽|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>命令動態屬性
 下列屬性會新增至 **命令** 物件的 **properties** 集合。

|ADO 屬性名稱|OLE DB 屬性名稱|
|-----------------------|--------------------------|
|存取順序|DBPROP_ACCESSORDER|
|封鎖儲存物件|DBPROP_BLOCKINGSTORAGEOBJECTS|
|書簽類型|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|變更插入的資料列|DBPROP_CHANGEINSERTEDROWS|
|資料行許可權|DBPROP_COLUMNRESTRICT|
|資料行集通知|DBPROP_NOTIFYCOLUMNSET|
|延遲儲存物件更新|DBPROP_DELAYSTORAGEOBJECTS|
|向後提取|DBPROP_CANFETCHBACKWARDS|
|保留資料列|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|Immobile 資料列|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsetLocate|
|IRowsetResynch||
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|常值書簽|DBPROP_LITERALBOOKMARKS|
|常值資料列識別|DBPROP_LITERALIDENTITY|
|開啟的資料列數上限|DBPROP_MAXOPENROWS|
|暫止的資料列數上限|DBPROP_MAXPENDINGROWS|
|最大資料列數|DBPROP_MAXROWS|
|通知細微性|DBPROP_NOTIFICATIONGRANULARITY|
|通知階段|DBPROP_NOTIFICATIONPHASES|
|物件交易|DBPROP_TRANSACTEDOBJECT|
|可見的變更|DBPROP_OWNUPDATEDELETE|
|擁有可見的插入|DBPROP_OWNINSERT|
|中止時保留|DBPROP_ABORTPRESERVE|
|在認可時保留|DBPROP_COMMITPRESERVE|
|快速重新開機|DBPROP_QUICKRESTART|
|重新進入事件|DBPROP_REENTRANTEVENTS|
|移除刪除的資料列|DBPROP_REMOVEDELETED|
|報告多項變更|DBPROP_REPORTMULTIPLECHANGES|
|傳回暫止的插入|DBPROP_RETURNPENDINGINSERTS|
|資料列刪除通知|DBPROP_NOTIFYROWDELETE|
|Row First 變更通知|DBPROP_NOTIFYROWFIRSTCHANGE|
|資料列插入通知|DBPROP_NOTIFYROWINSERT|
|資料列許可權|DBPROP_ROWRESTRICT|
|資料列重新同步通知|DBPROP_NOTIFYROWRESYNCH|
|資料列執行緒模型|DBPROP_ROWTHREADMODEL|
|資料列復原變更通知|DBPROP_NOTIFYROWUNDOCHANGE|
|資料列恢復刪除通知|DBPROP_NOTIFYROWUNDODELETE|
|資料列復原插入通知|DBPROP_NOTIFYROWUNDOINSERT|
|資料列更新通知|DBPROP_NOTIFYROWUPDATE|
|資料列集提取位置變更通知|DBPROP_NOTIFYROWSETFETCHPOSITIONCHANGE|
|資料列集發行通知|DBPROP_NOTIFYROWSETRELEASE|
|向後滾動|DBPROP_CANSCROLLBACKWARDS|
|略過已刪除的書簽|DBPROP_BOOKMARKSKIP|
|強式資料列識別|DBPROP_STRONGIDENTITY|
|更新|DBPROP_UPDATABILITY|
|使用書簽|DBPROP_BOOKMARKS|

 如需有關 Microsoft OLE DB Provider for ODBC 的特定執行與功能資訊的詳細資訊，請參閱 OLE DB 程式設計人員 [參考](/previous-versions/windows/desktop/ms713643(v=vs.85)) ，或造訪 MSDN 上的資料存取和儲存開發人員中心網站（英文）。

## <a name="see-also"></a>另請參閱
 [命令物件 (ado) ](../../reference/ado-api/command-object-ado.md) [COMMANDTEXT 屬性 (Ado) ](../../reference/ado-api/commandtext-property-ado.md) [連線物件 (ado) ](../../reference/ado-api/connection-object-ado.md) [ConnectionString 屬性 (ado) ](../../reference/ado-api/connectionstring-property-ado.md) [Execute 方法 (ado 命令) ](../../reference/ado-api/execute-method-ado-command.md) [Open 方法](../../reference/ado-api/open-method-ado-recordset.md) ([ado)  (](../../reference/ado-api/properties-collection-ado.md) [參數集合](../../reference/ado-api/parameters-collection-ado.md)) [ado (](../../reference/ado-api/recordset-object-ado.md) [提供者屬性](../../reference/ado-api/provider-property-ado.md)) [ado () ](../../reference/ado-api/supports-method.md)