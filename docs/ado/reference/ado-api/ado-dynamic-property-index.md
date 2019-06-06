---
title: ADO 動態屬性索引 |Microsoft Docs
ms.prod: sql
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- dynamic properties [ADO], index
ms.assetid: 80d389dd-46ef-459f-b0d4-6f712fc4f32d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8dd1263d19972124166e1e11d91c8370fc3a9ff0
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66696741"
---
# <a name="ado-dynamic-property-index"></a>ADO 動態屬性索引
資料提供者、 服務提供者，以及服務元件可以動態將屬性新增至**屬性**未開啟的集合[連線](../../../ado/reference/ado-api/connection-object-ado.md)並[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。 這些物件開啟時，指定提供者可能也會插入額外的屬性。 其中部分屬性所述[ADO 動態屬性](../../../ado/reference/ado-api/ado-dynamic-properties.md)一節。 多個列中的特定提供者在[附錄 a:提供者](../../../ado/guide/appendixes/appendix-a-providers.md)一節。  
  
 下表是 cross-indexes ADO 和 OLE DB 名稱的每個標準 OLE DB 提供者動態屬性。 您的提供者可以新增其他屬性，但是列出這裡。 如需提供者特有的動態屬性的特定資訊，請參閱您的提供者文件。  
  
 OLE DB 程式設計人員參考是參考的 ADO 屬性名稱的詞彙 「 描述 」。 如需有關這些標準屬性的詳細資訊，請搜尋或瀏覽中的索引[OLE DB 文件](https://msdn.microsoft.com/library/windows/desktop/ms722784.aspx)OLE DB 屬性名稱。  
  
## <a name="connection-dynamic-properties"></a>連接的動態屬性  
  
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
|傳址存取子|DBPROP_BYREFACCESSORS|  
|[密碼]|DBPROP_AUTH_PASSWORD|  
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
 請注意，**動態屬性**的**Recordset**物件超出範圍 （變成無法使用） 時移**資料錄集**已關閉。  
  
|ADO 屬性名稱|OLE DB 屬性名稱|  
|-----------------------|--------------------------|  
|IAccessor|DBPROP_IACCESSOR|  
|IChapteredRowset||  
|IColumnsInfo|DBPROP_ICOLUMNSINFO|  
|IColumnsRowset|DBPROP_ICOLUMNSROWSET|  
|IConnectionPointContainer|DBPROP_ICONNECTIONPOINTCONTAINER|  
|IConvertType||  
|ILockBytes|DBPROP_ILOCKBYTES|  
|IRowset|DBPROP_IROWSET|  
|IDBAsynchStatus|DBPROP_IDBASYNCHSTATUS|  
|IParentRowset||  
|IRowsetChange|DBPROP_IROWSETCHANGE|  
|IRowsetExactScroll||  
|IRowsetFind|DBPROP_IROWSETFIND|  
|IRowsetIdentity|DBPROP_IROWSETIDENTITY|  
|IRowsetInfo|DBPROP_IROWSETINFO|  
|IRowsetLocate|DBPROP_IROWSETLOCATE|  
|IRowsetRefresh|DBPROP_IROWSETREFRESH|  
|IRowsetResynch||  
|IRowsetScroll|DBPROP_IROWSETSCROLL|  
|IRowsetUpdate|DBPROP_IROWSETUPDATE|  
|IRowsetView|DBPROP_IROWSETVIEW|  
|IRowsetIndex|DBPROP_IROWSETINDEX|  
|ISequentialStream|DBPROP_ISEQUENTIALSTREAM|  
|IStorage|DBPROP_ISTORAGE|  
|IStream|DBPROP_ISTREAM|  
|ISupportErrorInfo|DBPROP_ISUPPORTERRORINFO|  
|存取順序|DBPROP_ACCESSORDER|  
|僅附加的資料列集|DBPROP_APPENDONLY|  
|非同步資料列集處理|DBPROP_ROWSET_ASYNCH|  
|自動重新計算|DBPROP_ADC_AUTORECALC|  
|背景提取大小|DBPROP_ASYNCHFETCHSIZE|  
|背景執行緒優先順序|DBPROP_ASYNCHTHREADPRIORITY|  
|批次大小|DBPROP_ADC_BATCHSIZE|  
|封鎖的儲存體物件|DBPROP_BLOCKINGSTORAGEOBJECTS|  
|書籤類型|DBPROP_BOOKMARKTYPE|  
|Bookmarkable|DBPROP_IROWSETLOCATE|  
|排序的書籤|DBPROP_ORDEREDBOOKMARKS|  
|快取子資料列|DBPROP_ADC_CACHECHILDROWS|  
|快取延後的資料行|DBPROP_CACHEDEFERRED|  
|變更插入的資料列|DBPROP_CHANGEINSERTEDROWS|  
|資料行權限|DBPROP_COLUMNRESTRICT|  
|資料行集告知|DBPROP_NOTIFYCOLUMNSET|  
|可寫入的資料行|DBPROP_MAYWRITECOLUMN|  
|命令逾時|DBPROP_COMMANDTIMEOUT|  
|資料指標引擎版本|DBPROP_ADC_CEVER|  
|延後資料行|DBPROP_DEFERRED|  
|延遲儲存物件更新|DBPROP_DELAYSTORAGEOBJECTS|  
|向後擷取|DBPROP_CANFETCHBACKWARDS|  
|篩選作業|DBPROP_FILTERCOMPAREOPS|  
|尋找作業|DBPROP_FINDCOMPAREOPS|  
|隱藏的資料行 （計數）|DBPROP_HIDDENCOLUMNS|  
|保留資料列|DBPROP_CANHOLDROWS|  
|固定的資料列|DBPROP_IMMOBILEROWS|  
|初始的提取大小|DBPROP_ASYNCHPREFETCHSIZE|  
|常值書籤|DBPROP_LITERALBOOKMARKS|  
|常值的資料列識別|DBPROP_LITERALIDENTITY|  
|維護變更狀態|DBPROP_ADC_MAINTAINCHANGESTATUS|  
|開啟資料列數上限|DBPROP_MAXOPENROWS|  
|暫止資料列的最大值|DBPROP_MAXPENDINGROWS|  
|最大資料列|DBPROP_MAXROWS|  
|記憶體使用量|DBPROP_MEMORYUSAGE|  
|告知細微性|DBPROP_NOTIFICATIONGRANULARITY|  
|告知階段|DBPROP_NOTIFICATIONPHASES|  
|物件已交易|DBPROP_TRANSACTEDOBJECT|  
|可見的其他變更|DBPROP_OTHERUPDATEDELETE|  
|可見的其他插入|DBPROP_OTHERINSERT|  
|可見的自我變更|DBPROP_OWNUPDATEDELETE|  
|可見的自我插入|DBPROP_OWNINSERT|  
|在中止上保留|DBPROP_ABORTPRESERVE|  
|在認可上保留|DBPROP_COMMITPRESERVE|  
|Private1||  
|快速重新啟動|DBPROP_QUICKRESTART|  
|可重新進入的事件|DBPROP_REENTRANTEVENTS|  
|移除已刪除的資料列|DBPROP_REMOVEDELETED|  
|報告多重變更|DBPROP_REPORTMULTIPLECHANGES|  
|調整形狀名稱|DBPROP_ADC_RESHAPENAME|  
|重新同步命令|DBPROP_ADC_CUSTOMRESYNCH|  
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
|伺服器資料指標|DBPROP_SERVERCURSOR|  
|略過刪除書籤|DBPROP_BOOKMARKSKIPPED|  
|強式資料列識別|DBPROP_STRONGIDENTITY|  
|唯一的目錄|DBPROP_ADC_UNIQUECATALOG|  
|唯一資料列|DBPROP_UNIQUEROWS|  
|唯一的結構描述|DBPROP_ADC_UNIQUESCHEMA|  
|Unique Table|DBPROP_ADC_UNIQUETABLE|  
|可更新性|DBPROP_UPDATABILITY|  
|更新準則|DBPROP_ADC_UPDATECRITERIA|  
|更新重新同步處理|DBPROP_ADC_UPDATERESYNC|  
|使用書籤|DBPROP_BOOKMARKS|
