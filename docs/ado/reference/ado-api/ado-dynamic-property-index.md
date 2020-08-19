---
description: ADO 動態屬性索引
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
author: rothja
ms.author: jroth
ms.openlocfilehash: fbd7933ac206f81460a7d0d50d0a7ac332cf154a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451460"
---
# <a name="ado-dynamic-property-index"></a>ADO 動態屬性索引
資料提供者、服務提供者和服務元件可以將動態屬性加入至未開啟之[連接](../../../ado/reference/ado-api/connection-object-ado.md)和[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件的**屬性**集合。 當這些物件開啟時，指定的提供者也可以插入其他屬性。 其中一些屬性會列在 [ [ADO 動態屬性](../../../ado/reference/ado-api/ado-dynamic-properties.md) ] 區段中。 [ [附錄 A：提供者](../../../ado/guide/appendixes/appendix-a-providers.md) ] 一節中的特定提供者底下會列出更多。  
  
 下表是每個標準 OLE DB 提供者動態屬性的 ADO 和 OLE DB 名稱的交叉索引。 您的提供者可能會新增超過此處所列的屬性。 如需提供者特定動態屬性的相關資訊，請參閱您的提供者檔。  
  
 OLE DB 程式設計人員參考是依「描述」一詞來參考 ADO 屬性名稱。 如需這些標準屬性的詳細資訊，請在 OLE DB 屬性的 [OLE DB 檔](https://msdn.microsoft.com/library/windows/desktop/ms722784.aspx)中搜尋或流覽索引（依名稱）。  
  
## <a name="connection-dynamic-properties"></a>連接動態屬性  
  
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
|以 Ref 存取子傳遞|DBPROP_BYREFACCESSORS|  
|密碼|DBPROP_AUTH_PASSWORD|  
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
 請注意 **，記錄集物件的****動態屬性**超出範圍 (在關閉**記錄集**時變成無法使用) 。  
  
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
|封鎖儲存物件|DBPROP_BLOCKINGSTORAGEOBJECTS|  
|書簽類型|DBPROP_BOOKMARKTYPE|  
|Bookmarkable|DBPROP_IROWSETLOCATE|  
|排序的書簽|DBPROP_ORDEREDBOOKMARKS|  
|快取子資料列|DBPROP_ADC_CACHECHILDROWS|  
|快取延遲的資料行|DBPROP_CACHEDEFERRED|  
|變更插入的資料列|DBPROP_CHANGEINSERTEDROWS|  
|資料行許可權|DBPROP_COLUMNRESTRICT|  
|資料行集通知|DBPROP_NOTIFYCOLUMNSET|  
|資料行可寫入|DBPROP_MAYWRITECOLUMN|  
|命令逾時|DBPROP_COMMANDTIMEOUT|  
|資料指標引擎版本|DBPROP_ADC_CEVER|  
|延遲資料行|DBPROP_DEFERRED|  
|延遲儲存物件更新|DBPROP_DELAYSTORAGEOBJECTS|  
|向後提取|DBPROP_CANFETCHBACKWARDS|  
|篩選作業|DBPROP_FILTERCOMPAREOPS|  
|尋找作業|DBPROP_FINDCOMPAREOPS|  
|隱藏的資料行 (計數) |DBPROP_HIDDENCOLUMNS|  
|保留資料列|DBPROP_CANHOLDROWS|  
|Immobile 資料列|DBPROP_IMMOBILEROWS|  
|初始提取大小|DBPROP_ASYNCHPREFETCHSIZE|  
|常值書簽|DBPROP_LITERALBOOKMARKS|  
|常值資料列識別|DBPROP_LITERALIDENTITY|  
|維護變更狀態|DBPROP_ADC_MAINTAINCHANGESTATUS|  
|開啟的資料列數上限|DBPROP_MAXOPENROWS|  
|暫止的資料列數上限|DBPROP_MAXPENDINGROWS|  
|最大資料列數|DBPROP_MAXROWS|  
|記憶體使用量|DBPROP_MEMORYUSAGE|  
|通知細微性|DBPROP_NOTIFICATIONGRANULARITY|  
|通知階段|DBPROP_NOTIFICATIONPHASES|  
|物件交易|DBPROP_TRANSACTEDOBJECT|  
|他人的變更可見|DBPROP_OTHERUPDATEDELETE|  
|其他人的插入可見|DBPROP_OTHERINSERT|  
|可見的變更|DBPROP_OWNUPDATEDELETE|  
|擁有可見的插入|DBPROP_OWNINSERT|  
|中止時保留|DBPROP_ABORTPRESERVE|  
|在認可時保留|DBPROP_COMMITPRESERVE|  
|Private1||  
|快速重新開機|DBPROP_QUICKRESTART|  
|重新進入事件|DBPROP_REENTRANTEVENTS|  
|移除刪除的資料列|DBPROP_REMOVEDELETED|  
|報告多項變更|DBPROP_REPORTMULTIPLECHANGES|  
|重新調整名稱|DBPROP_ADC_RESHAPENAME|  
|Resync 命令|DBPROP_ADC_CUSTOMRESYNCH|  
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
|伺服器資料指標|DBPROP_SERVERCURSOR|  
|略過已刪除的書簽|DBPROP_BOOKMARKSKIPPED|  
|強式資料列識別|DBPROP_STRONGIDENTITY|  
|唯一目錄|DBPROP_ADC_UNIQUECATALOG|  
|唯一資料列|DBPROP_UNIQUEROWS|  
|唯一架構|DBPROP_ADC_UNIQUESCHEMA|  
|Unique Table|DBPROP_ADC_UNIQUETABLE|  
|更新|DBPROP_UPDATABILITY|  
|更新準則|DBPROP_ADC_UPDATECRITERIA|  
|更新重新同步|DBPROP_ADC_UPDATERESYNC|  
|使用書簽|DBPROP_BOOKMARKS|
