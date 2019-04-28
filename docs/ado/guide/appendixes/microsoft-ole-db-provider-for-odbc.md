---
title: Microsoft OLE DB Provider for ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e75b79934022743ba806722427dd37ab733bc2f2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62853325"
---
# <a name="microsoft-ole-db-provider-for-odbc-overview"></a>Microsoft OLE DB Provider for ODBC 概觀
ADO 或 RDS 程式設計人員，理想的世界就是每個資料來源會公開 OLE DB 介面，可讓 ADO 無法呼叫直接將資料來源。 雖然有更多資料庫廠商實作的 OLE DB 介面，但某些資料來源不是尚未公開這種方式。 不過，大部分的 DBMS 系統目前使用中可以透過 ODBC 存取。

 ODBC 驅動程式可供非 Microsoft 資料庫產品，例如 Oracle 除了包含 Microsoft SQL Server、 Microsoft Access （Microsoft Jet 資料庫引擎） 和 Microsoft FoxPro，每個主要 DBMS 目前使用中。

 Microsoft ODBC 提供者，不過，可讓 ADO 連接到任何 ODBC 資料來源。 提供者是無限制執行緒，並啟用 Unicode。

 提供者支援交易，但不同的 DBMS 引擎提供不同類型的交易支援。 例如，Microsoft Access 支援最多五個層級深度的巢狀的交易。

 這是預設的提供者的 ADO 中，並支援所有的提供者相依的 ADO 屬性和方法。

## <a name="connection-string-parameters"></a>連接字串參數
 若要連接到此提供者，將**提供者 =** 引數[ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md)屬性：

```
MSDASQL
```

 讀取[提供者](../../../ado/reference/ado-api/provider-property-ado.md)屬性會傳回此字串以及。

## <a name="typical-connection-string"></a>一般連接字串
 此提供者的一般連接字串是：

```
"Provider=MSDASQL;DSN=dsnName;UID=MyUserID;PWD=MyPassword;"
```

 字串是由這些關鍵字所組成：

|關鍵字|描述|
|-------------|-----------------|
|**提供者**|指定的 OLE DB provider for ODBC。|
|**DSN**|指定資料來源的名稱。|
|**UID**|指定使用者名稱。|
|**PWD**|指定使用者密碼。|
|**URL**|指定的檔案或目錄已發佈 Web 資料夾中的 URL。|

 因為這是預設的提供者的 ADO 中，如果您省略**提供者 =** 參數從連接字串，ADO 會嘗試連接到此提供者。

> [!NOTE]
>  如果您要連接到資料來源提供者支援 Windows 驗證，您應該指定**Trusted_Connection = yes**或是**Integrated Security = SSPI**而非使用者 ID 和密碼連接字串中的資訊。

 提供者不支援任何特定的連接參數，除了 ADO 所定義。 不過，提供者會將任何非 ADO 連接參數傳遞至 ODBC 驅動程式管理員。

 因為您可以省略**提供者**參數，您可以因此撰寫等同於相同的資料來源的 ODBC 連接字串的 ADO 連接字串。 使用相同的參數名稱 (**驅動程式 =**， **DATABASE =**， **DSN =** 等等)，值，以及與您的語法會撰寫的 ODBC 連接字串時。 您可以在包含或不含預先定義的資料來源名稱 (DSN) 或 FileDSN 連接。

## <a name="syntax-with-a-dsn-or-filedsn"></a>使用資料來源名稱或 FileDSN 語法：

```
"[Provider=MSDASQL;] { DSN=name | FileDSN=filename } ;
[DATABASE=database;] UID=user; PWD=password"
```

## <a name="syntax-without-a-dsn-dsn-less-connection"></a>語法，但是沒有資料來源名稱 （無 DSN 連接）：

```
"[Provider=MSDASQL;] DRIVER=driver; SERVER=server;
DATABASE=database; UID=MyUserID; PWD=MyPassword"
```

## <a name="remarks"></a>備註
 如果您使用**DSN**或是**FileDSN**，它必須定義透過 ODBC 資料來源管理員在 Windows 控制台中。 在 Microsoft Windows 2000 中，ODBC 管理員位於 系統管理工具。 在舊版的 Windows 中，名為 ODBC 管理員圖示**32 位元 ODBC**或簡稱**ODBC**。

 設定替代**DSN**，您可以指定 ODBC 驅動程式 (**驅動程式 =**)，例如"SQL Server"; 伺服器名稱 (**SERVER =**); 和資料庫名稱 (**DATABASE =**)。

 您也可以指定使用者帳戶名稱 (**UID =**)，以及使用者帳戶的密碼 (**PWD =**) 或標準 ODBC 特有的參數中 ADO 定義*使用者*和*密碼*參數。

 雖然**DSN**已定義指定的資料庫，您可以指定 *資料庫*參數，除了**DSN**連線不同的資料庫。 最好一律包括 *資料庫*當您使用的參數**DSN**。 這可確保您連線到正確的資料庫，如果另一位使用者變更預設資料庫參數，因為您上次檢查**DSN**定義。

## <a name="provider-specific-connection-properties"></a>提供者特定連接屬性
 OLE DB provider for ODBC 數個將屬性加入至[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)的集合**連線**物件。 下表列出這些屬性與對應的 OLE DB 屬性名稱括號括住。

|屬性名稱|描述|
|-------------------|-----------------|
|可存取的程序 (KAGPROP_ACCESSIBLEPROCEDURES)|指出使用者是否有預存程序的存取。|
|可存取的資料表 (KAGPROP_ACCESSIBLETABLES)|指出使用者是否有執行對資料庫資料表的 SELECT 陳述式的權限。|
|作用中陳述式 (KAGPROP_ACTIVESTATEMENTS)|指出 ODBC 驅動程式可以在連接支援的控制代碼數目。|
|驅動程式名稱 (KAGPROP_DRIVERNAME)|指出 ODBC 驅動程式的檔案名稱。|
|驅動程式的 ODBC 版本 (KAGPROP_DRIVERODBCVER)|指出此驅動程式支援的 ODBC 版本。|
|檔案使用情況 (KAGPROP_FILEUSAGE)|指出如何驅動程式會將資料來源; 中的檔案為資料表，或為類別目錄。|
|Like 逸出子句 (KAGPROP_LIKEESCAPECLAUSE)|指出是否此驅動程式支援的定義和逸出字元使用百分比字元 （%）與 LIKE 述詞的 WHERE 子句加上底線字元 (_)。|
|在 群組依據 (KAGPROP_MAXCOLUMNSINGROUPBY) 的最大資料行|表示可以在 SELECT 陳述式的 GROUP BY 子句中列出的資料行的數目上限。|
|索引 (KAGPROP_MAXCOLUMNSININDEX) 中的最大資料行|指出索引中所包含的資料行的數目上限。|
|Order By (KAGPROP_MAXCOLUMNSINORDERBY) 中的最大資料行|表示可以在 SELECT 陳述式的 ORDER BY 子句中列出的資料行的數目上限。|
|在 選取 (KAGPROP_MAXCOLUMNSINSELECT) 的最大資料行|表示可以在 SELECT 陳述式的 SELECT 部分中列出的資料行的數目上限。|
|資料表 (KAGPROP_MAXCOLUMNSINTABLE) 中的最大資料行|表示允許在資料表中的資料行數目上限。|
|數值函式 (KAGPROP_NUMERICFUNCTIONS)|指出 ODBC 驅動程式支援的數值函式。 如需函式名稱和相關聯的值，這個位元遮罩中所使用的清單，請參閱[附錄 e:純量函數](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)，ODBC 文件中。|
|外部聯結功能 (KAGPROP_OJCAPABILITY)|指出提供者支援外部聯結的類型。|
|外部聯結 (KAGPROP_OUTERJOINS)|指出提供者是否支援外部聯結。|
|特殊字元 (KAGPROP_SPECIALCHARACTERS)|指出哪些字元有特殊的意義，ODBC 驅動程式。|
|預存程序 (KAGPROP_PROCEDURES)|指出預存程序是否可用於此 ODBC 驅動程式。|
|字串函數 (KAGPROP_STRINGFUNCTIONS)|指出 ODBC 驅動程式支援哪些字串函式。 如需函式名稱和相關聯的值，這個位元遮罩中所使用的清單，請參閱[附錄 e:純量函數](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)，ODBC 文件中。|
|系統函式 (KAGPROP_SYSTEMFUNCTIONS)|指出 ODBC 驅動程式支援哪些系統函式。 如需函式名稱和相關聯的值，這個位元遮罩中所使用的清單，請參閱[附錄 e:純量函數](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)，ODBC 文件中。|
|日期/時間函式 (KAGPROP_TIMEDATEFUNCTIONS)|指出 ODBC 驅動程式支援的日期和時間函數。 如需函式名稱和相關聯的值，這個位元遮罩中所使用的清單，請參閱[附錄 e:純量函數](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)，ODBC 文件中。|
|SQL 文法支援 (KAGPROP_ODBCSQLCONFORMANCE)|指出 ODBC 驅動程式支援的 SQL 文法。|

## <a name="provider-specific-recordset-and-command-properties"></a>提供者特定資料錄集和命令屬性
 OLE DB provider for ODBC 數個將屬性加入至**屬性**的集合**資料錄集**並**命令**物件。 下表列出這些屬性與對應的 OLE DB 屬性名稱括號括住。

|屬性名稱|描述|
|-------------------|-----------------|
|查詢為基礎的更新/刪除/插入 (KAGPROP_QUERYBASEDUPDATES)|指出是否執行更新、 刪除和插入作業所使用的 SQL 查詢。|
|ODBC 並行類型 (KAGPROP_CONCURRENCY)|表示用來減少兩位使用者嘗試同時存取相同的資料從資料來源所造成的潛在問題的方法。|
|順向資料指標 (KAGPROP_BLOBSONFOCURSOR) 上的 BLOB 存取範圍|指出是否 BLOB**欄位**使用順向資料指標時，可以存取。|
|SQL_FLOAT、 SQL_DOUBLE 和 SQL_REAL 納入 QBU WHERE 子句 (KAGPROP_INCLUDENONEXACT)|指出是否 SQL_FLOAT、 SQL_DOUBLE 和 SQL_REAL 值可以包含在 QBU WHERE 子句中。|
|在 插入 (KAGPROP_POSITIONONNEWROW) 後的最後一個資料列上的位置|表示已在資料表中插入新記錄之後，資料表中的最後一個資料列會出現在目前資料列。|
|IRowsetChangeExtInfo (KAGPROP_IROWSETCHANGEEXTINFO)|指出是否**IRowsetChange**介面提供的擴充的資訊的支援。|
|ODBC 資料指標類型 (KAGPROP_CURSOR)|表示所使用的資料指標類型**資料錄集**。|
|產生可以封送處理的資料列集 (KAGPROP_MARSHALLABLE)|指出 ODBC 驅動程式會產生可以封送處理的資料錄集|

## <a name="command-text"></a>命令文字
 您的使用方式[命令](../../../ado/reference/ado-api/command-object-ado.md)物件主要取決於資料來源，並將接受查詢或命令的陳述式的類型。

 ODBC 會提供特定的語法來呼叫預存程序。 針對[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)屬性**命令**物件*CommandText*引數**Execute**方法[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件，或有*來源*引數**開啟**方法[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件，在字串中使用此語法的階段：

```
"{ [ ? = ] call procedure [ ( ? [, ? [ , ... ]] ) ] }"
```

 每個**嗎？** 參考的物件[參數](../../../ado/reference/ado-api/parameters-collection-ado.md)集合。 第一個**嗎？** 參考**參數**(0)，下一步**嗎？** 參考**參數**(1)，依此類推。

 參數參考是選擇性的取決於預存程序的結構。 如果您想要呼叫未定義任何參數的預存程序，您的字串看起來會如下所示：

```
"{ call procedure }"
```

 如果您有兩個查詢參數時，您的字串會如下所示：

```
"{ call procedure ( ?, ? ) }"
```

 如果預存程序會傳回值，傳回的值會被視為另一個參數中。 如果您有任何查詢參數，但沒有傳回值，您的字串會如下所示：

```
"{ ? = call procedure }"
```

 最後，如果您有一個傳回值，而且兩個查詢參數，您的字串會如下所示：

```
"{ ? = call procedure ( ?, ? ) }"
```

## <a name="recordset-behavior"></a>資料錄集行為
 下表列出標準的 ADO 方法和屬性上可用**資料錄集**開啟與此提供者的物件。

 如需詳細資訊的相關**資料錄集**您的提供者組態，執行行為[支援](../../../ado/reference/ado-api/supports-method.md)方法，並列舉**屬性**的集合**資料錄集**來判斷提供者特有的動態屬性是否存在。

 標準的 ADO 的可用性**資料錄集**屬性：

|屬性|ForwardOnly|動態|索引鍵集|Static|
|--------------|-----------------|-------------|------------|------------|
|[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)|無法使用|無法使用|讀取/寫入|讀取/寫入|
|[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)|無法使用|無法使用|讀取/寫入|讀取/寫入|
|[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)|讀取/寫入|讀取/寫入|讀取/寫入|讀取/寫入|
|[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)|唯讀|唯讀|唯讀|唯讀|
|[Bookmark](../../../ado/reference/ado-api/bookmark-property-ado.md)|無法使用|無法使用|讀取/寫入|讀取/寫入|
|[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)|讀取/寫入|讀取/寫入|讀取/寫入|讀取/寫入|
|[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)|讀取/寫入|讀取/寫入|讀取/寫入|讀取/寫入|
|[CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)|讀取/寫入|讀取/寫入|讀取/寫入|讀取/寫入|
|[EditMode](../../../ado/reference/ado-api/editmode-property.md)|唯讀|唯讀|唯讀|唯讀|
|[篩選](../../../ado/reference/ado-api/filter-property.md)|讀取/寫入|讀取/寫入|讀取/寫入|讀取/寫入|
|[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)|讀取/寫入|讀取/寫入|讀取/寫入|讀取/寫入|
|[MarshalOptions](../../../ado/reference/ado-api/marshaloptions-property-ado.md)|讀取/寫入|讀取/寫入|讀取/寫入|讀取/寫入|
|[MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)|讀取/寫入|讀取/寫入|讀取/寫入|讀取/寫入|
|[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)|讀取/寫入|無法使用|唯讀|唯讀|
|[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)|讀取/寫入|讀取/寫入|讀取/寫入|讀取/寫入|
|[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)|讀取/寫入|無法使用|唯讀|唯讀|
|[Source](../../../ado/reference/ado-api/source-property-ado-recordset.md)|讀取/寫入|讀取/寫入|讀取/寫入|讀取/寫入|
|[狀態](../../../ado/reference/ado-api/state-property-ado.md)|唯讀|唯讀|唯讀|唯讀|
|[狀態](../../../ado/reference/ado-api/status-property-ado-recordset.md)|唯讀|唯讀|唯讀|唯讀|

 [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)並[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)屬性是唯寫 ADO 使用 1.0 版的 Microsoft OLE DB Provider for ODBC 時。

 標準的 ADO 的可用性**資料錄集**方法：

|方法|ForwardOnly|動態|索引鍵集|Static|
|------------|-----------------|-------------|------------|------------|
|[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)|是|是|是|是|
|[取消](../../../ado/reference/ado-api/cancel-method-ado.md)|是|是|是|是|
|[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)|是|是|是|是|
|[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)|是|是|是|是|
|[複製](../../../ado/reference/ado-api/clone-method-ado.md)|否|否|是|是|
|[關閉](../../../ado/reference/ado-api/close-method-ado.md)|是|是|是|是|
|[刪除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)|是|是|是|是|
|[GetRows](../../../ado/reference/ado-api/getrows-method-ado.md)|是|是|是|是|
|[[移動]](../../../ado/reference/ado-api/move-method-ado.md)|是|是|是|是|
|[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|是|是|是|是|
|[MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|否|是|是|是|
|[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|是|是|是|是|
|[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|否|是|是|是|
|[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)*|是|是|是|是|
|[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)|是|是|是|是|
|[重新查詢](../../../ado/reference/ado-api/requery-method.md)|是|是|是|是|
|[重新同步處理](../../../ado/reference/ado-api/resync-method.md)|否|否|是|是|
|[支援](../../../ado/reference/ado-api/supports-method.md)|是|是|是|是|
|[Update](../../../ado/reference/ado-api/update-method.md)|是|是|是|是|
|[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)|是|是|是|是|

 * 不支援針對 Microsoft Access 資料庫。

## <a name="dynamic-properties"></a>動態屬性
 Microsoft OLE DB Provider for ODBC 插入到數個動態屬性**屬性**未開啟的集合[連線](../../../ado/reference/ado-api/connection-object-ado.md)，[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)，以及[命令](../../../ado/reference/ado-api/command-object-ado.md)物件。

 下表是 cross-index 的 ADO 和 OLE DB 的名稱，為每個動態屬性。 OLE DB 程式設計人員參考是參考的 ADO 屬性名稱的詞彙，「 說明 」。 您可以在 OLE DB 程式設計人員參考中找到這些屬性的詳細資訊。 搜尋索引中的 OLE DB 屬性名稱，或參閱[附錄 c:OLE DB 屬性](https://msdn.microsoft.com/deded3ff-f508-4e1b-b2b1-fd9afd3bd292)。

## <a name="connection-dynamic-properties"></a>連接的動態屬性
 下列屬性會新增至**連接**物件的**屬性**集合。

|ADO 屬性名稱|OLE DB 屬性名稱|
|-----------------------|--------------------------|
|Active Sessions|DBPROP_ACTIVESESSIONS|
|非同步中止|DBPROP_ASYNCTXNABORT|
|非同步認可|DBPROP_ASYNCTNXCOMMIT|
|自動認可隔離等級|DBPROP_SESS_AUTOCOMMITISOLEVELS|
|目錄位置|DBPROP_CATALOGLOCATION|
|資料目錄詞彙|DBPROP_CATALOGTERM|
|資料行定義|DBPROP_COLUMNDEFINITION|
|連接逾時|DBPROP_INIT_TIMEOUT|
|目前的目錄|DBPROP_CURRENTCATALOG|
|資料來源|DBPROP_INIT_DATASOURCE|
|資料來源名稱|DBPROP_DATASOURCENAME|
|資料來源物件執行緒模型|DBPROP_DSOTHREADMODEL|
|DBMS 名稱|DBPROP_DBMSNAME|
|DBMS 版本|DBPROP_DBMSVER|
|擴充屬性|DBPROP_INIT_PROVIDERSTRING|
|GROUP BY 支援|DBPROP_GROUPBY|
|異質性資料表支援|DBPROP_HETEROGENEOUSTABLES|
|識別項區分大小寫|DBPROP_IDENTIFIERCASE|
|初始目錄|DBPROP_INIT_CATALOG|
|隔離等級|DBPROP_SUPPORTEDTXNISOLEVELS|
|隔離保留功能|DBPROP_SUPPORTEDTXNISORETAIN|
|地區設定識別碼|DBPROP_INIT_LCID|
|Location|DBPROP_INIT_LOCATION|
|索引大小上限|DBPROP_MAXINDEXSIZE|
|資料列大小上限|DBPROP_MAXROWSIZE|
|資料列大小上限包括 BLOB|DBPROP_MAXROWSIZEINCLUDESBLOB|
|在選取的最大資料表|DBPROP_MAXTABLESINSELECT|
|模式|DBPROP_INIT_MODE|
|多個參數集|DBPROP_MULTIPLEPARAMSETS|
|多個結果|DBPROP_MULTIPLERESULTS|
|多個儲存體物件|DBPROP_MULTIPLESTORAGEOBJECTS|
|多重資料表更新|DBPROP_MULTITABLEUPDATE|
|NULL 定序排序|DBPROP_NULLCOLLATION|
|NULL 串連行為|DBPROP_CONCATNULLBEHAVIOR|
|OLE DB 服務|DBPROP_INIT_OLEDBSERVICES|
|OLE DB 版本|DBPROP_PROVIDEROLEDBVER|
|OLE 物件支援|DBPROP_OLEOBJECTS|
|開啟資料列集支援|DBPROP_OPENROWSETSUPPORT|
|ORDER BY 選取清單中的資料行|DBPROP_ORDERBYCOLUMNSINSELECT|
|輸出參數使用|DBPROP_OUTPUTPARAMETERAVAILABILITY|
|[密碼]|DBPROP_AUTH_PASSWORD|
|傳址存取子|DBPROP_BYREFACCESSORS|
|保存安全性資訊|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|
|持續性 ID 類型|DBPROP_PERSISTENTIDTYPE|
|準備中止行為|DBPROP_PREPAREABORTBEHAVIOR|
|準備認可行為|DBPROP_PREPARECOMMITBEHAVIOR|
|程序詞彙|DBPROP_PROCEDURETERM|
|提示|DBPROP_INIT_PROMPT|
|提供者易記名稱|DBPROP_PROVIDERFRIENDLYNAME|
|Provider Name|DBPROP_PROVIDERFILENAME|
|提供者版本|DBPROP_PROVIDERVER|
|唯讀資料來源|DBPROP_DATASOURCEREADONLY|
|在命令上的資料列集轉換|DBPROP_ROWSETCONVERSIONSONCOMMAND|
|結構描述詞彙|DBPROP_SCHEMATERM|
|結構描述使用方式|DBPROP_SCHEMAUSAGE|
|SQL 支援|DBPROP_SQLSUPPORT|
|結構化儲存體|DBPROP_STRUCTUREDSTORAGE|
|子查詢支援|DBPROP_SUBQUERIES|
|資料表詞彙|DBPROP_TABLETERM|
|交易 DDL|DBPROP_SUPPORTEDTXNDDL|
|使用者識別碼|DBPROP_AUTH_USERID|
|使用者名稱|DBPROP_USERNAME|
|視窗控制代碼|DBPROP_INIT_HWND|

## <a name="recordset-dynamic-properties"></a>資料錄集動態屬性
 下列屬性會新增至**Recordset**物件的**屬性**集合。

|ADO 屬性名稱|OLE DB 屬性名稱|
|-----------------------|--------------------------|
|存取順序|DBPROP_ACCESSORDER|
|封鎖的儲存體物件|DBPROP_BLOCKINGSTORAGEOBJECTS|
|書籤類型|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|變更插入的資料列|DBPROP_CHANGEINSERTEDROWS|
|資料行權限|DBPROP_COLUMNRESTRICT|
|資料行集告知|DBPROP_NOTIFYCOLUMNSET|
|延遲儲存物件更新|DBPROP_DELAYSTORAGEOBJECTS|
|向後擷取|DBPROP_CANFETCHBACKWARDS|
|保留資料列|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|固定的資料列|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsetLocate|
|IRowsetResynch||
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|常值書籤|DBPROP_LITERALBOOKMARKS|
|常值的資料列識別|DBPROP_LITERALIDENTITY|
|開啟資料列數上限|DBPROP_MAXOPENROWS|
|暫止資料列的最大值|DBPROP_MAXPENDINGROWS|
|最大資料列|DBPROP_MAXROWS|
|告知細微性|DBPROP_NOTIFICATIONGRANULARITY|
|告知階段|DBPROP_NOTIFICATIONPHASES|
|物件已交易|DBPROP_TRANSACTEDOBJECT|
|可見的自我變更|DBPROP_OWNUPDATEDELETE|
|可見的自我插入|DBPROP_OWNINSERT|
|在中止上保留|DBPROP_ABORTPRESERVE|
|在認可上保留|DBPROP_COMMITPRESERVE|
|快速重新啟動|DBPROP_QUICKRESTART|
|可重新進入的事件|DBPROP_REENTRANTEVENTS|
|移除已刪除的資料列|DBPROP_REMOVEDELETED|
|報告多重變更|DBPROP_REPORTMULTIPLECHANGES|
|傳回暫止插入|DBPROP_RETURNPENDINGINSERTS|
|資料列刪除告知|DBPROP_NOTIFYROWDELETE|
|資料列的第一個變更告知|DBPROP_NOTIFYROWFIRSTCHANGE|
|資料列插入告知|DBPROP_NOTIFYROWINSERT|
|資料列的權限|DBPROP_ROWRESTRICT|
|資料列重新同步處理告知|DBPROP_NOTIFYROWRESYNCH|
|執行緒模型的資料列|DBPROP_ROWTHREADMODEL|
|資料列復原變更告知|DBPROP_NOTIFYROWUNDOCHANGE|
|資料列復原刪除告知|DBPROP_NOTIFYROWUNDODELETE|
|資料列復原插入告知|DBPROP_NOTIFYROWUNDOINSERT|
|資料列更新告知|DBPROP_NOTIFYROWUPDATE|
|資料列集擷取位置變更告知|DBPROP_NOTIFYROWSETFETCHPOSISIONCHANGE|
|資料列集發行告知|DBPROP_NOTIFYROWSETRELEASE|
|向後捲動|DBPROP_CANSCROLLBACKWARDS|
|略過刪除書籤|DBPROP_BOOKMARKSKIPPED|
|強式資料列識別|DBPROP_STRONGITDENTITY|
|唯一資料列|DBPROP_UNIQUEROWS|
|可更新性|DBPROP_UPDATABILITY|
|使用書籤|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>命令動態屬性
 下列屬性會新增至**命令**物件的**屬性**集合。

|ADO 屬性名稱|OLE DB 屬性名稱|
|-----------------------|--------------------------|
|存取順序|DBPROP_ACCESSORDER|
|封鎖的儲存體物件|DBPROP_BLOCKINGSTORAGEOBJECTS|
|書籤類型|DBPROP_BOOKMARKTYPE|
|Bookmarkable|DBPROP_IROWSETLOCATE|
|變更插入的資料列|DBPROP_CHANGEINSERTEDROWS|
|資料行權限|DBPROP_COLUMNRESTRICT|
|資料行集告知|DBPROP_NOTIFYCOLUMNSET|
|延遲儲存物件更新|DBPROP_DELAYSTORAGEOBJECTS|
|向後擷取|DBPROP_CANFETCHBACKWARDS|
|保留資料列|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|固定的資料列|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsetLocate|
|IRowsetResynch||
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|常值書籤|DBPROP_LITERALBOOKMARKS|
|常值的資料列識別|DBPROP_LITERALIDENTITY|
|開啟資料列數上限|DBPROP_MAXOPENROWS|
|暫止資料列的最大值|DBPROP_MAXPENDINGROWS|
|最大資料列|DBPROP_MAXROWS|
|告知細微性|DBPROP_NOTIFICATIONGRANULARITY|
|告知階段|DBPROP_NOTIFICATIONPHASES|
|物件已交易|DBPROP_TRANSACTEDOBJECT|
|可見的自我變更|DBPROP_OWNUPDATEDELETE|
|可見的自我插入|DBPROP_OWNINSERT|
|在中止上保留|DBPROP_ABORTPRESERVE|
|在認可上保留|DBPROP_COMMITPRESERVE|
|快速重新啟動|DBPROP_QUICKRESTART|
|可重新進入的事件|DBPROP_REENTRANTEVENTS|
|移除已刪除的資料列|DBPROP_REMOVEDELETED|
|報告多重變更|DBPROP_REPORTMULTIPLECHANGES|
|傳回暫止插入|DBPROP_RETURNPENDINGINSERTS|
|資料列刪除告知|DBPROP_NOTIFYROWDELETE|
|資料列的第一個變更告知|DBPROP_NOTIFYROWFIRSTCHANGE|
|資料列插入告知|DBPROP_NOTIFYROWINSERT|
|資料列的權限|DBPROP_ROWRESTRICT|
|資料列重新同步處理告知|DBPROP_NOTIFYROWRESYNCH|
|執行緒模型的資料列|DBPROP_ROWTHREADMODEL|
|資料列復原變更告知|DBPROP_NOTIFYROWUNDOCHANGE|
|資料列復原刪除告知|DBPROP_NOTIFYROWUNDODELETE|
|資料列復原插入告知|DBPROP_NOTIFYROWUNDOINSERT|
|資料列更新告知|DBPROP_NOTIFYROWUPDATE|
|資料列集擷取位置變更告知|DBPROP_NOTIFYROWSETFETCHPOSITIONCHANGE|
|資料列集發行告知|DBPROP_NOTIFYROWSETRELEASE|
|向後捲動|DBPROP_CANSCROLLBACKWARDS|
|略過刪除書籤|DBPROP_BOOKMARKSKIP|
|強式資料列識別|DBPROP_STRONGIDENTITY|
|可更新性|DBPROP_UPDATABILITY|
|使用書籤|DBPROP_BOOKMARKS|

 如需有關特定實作和有關 Microsoft OLE DB Provider for ODBC 的功能資訊的詳細資訊，請參閱 < [OLE DB 程式設計人員參考](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8)或瀏覽 MSDN 上的資料存取和儲存體開發人員中心網站。

## <a name="see-also"></a>另請參閱
 [命令物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md) [CommandText 屬性 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md) [連接物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) [ConnectionString 屬性 (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [執行方法 (ADO Command)](../../../ado/reference/ado-api/execute-method-ado-command.md) [Open 方法 (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md) [Parameters 集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md) [屬性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md) [提供者屬性 (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [支援方法](../../../ado/reference/ado-api/supports-method.md)
