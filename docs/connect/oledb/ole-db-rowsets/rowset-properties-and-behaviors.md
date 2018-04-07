---
title: 資料列集屬性和行為 |Microsoft 文件
description: 資料列集屬性和 OLE DB 驅動程式的 SQL Server 中的行為
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], properties
- OLE DB Driver for SQL Server, rowsets
- properties [OLE DB]
- OLE DB rowsets, properties
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6724a1f7123be2040fd87d4a14ca4b45b7eb99ee
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/06/2018
---
# <a name="rowset-properties-and-behaviors"></a>資料列集屬性和行為
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  這些是 SQL Server 資料列集屬性，OLE DB 驅動程式。  
  
|屬性識別碼|Description|  
|-----------------|-----------------|  
|DBPROP_ABORTPRESERVE|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述：中止操作後的資料列集行為取決於此屬性。<br /><br /> VARIANT_FALSE: SQL Server OLE DB 驅動程式，使資料列集失效之後中止作業。 資料列集物件的功能都會幾乎遺失。 它只支援**IUnknown**作業和未處理的資料列與存取子控制代碼的版本。<br /><br /> VARIANT_TRUE: SQL Server OLE DB 驅動程式會維護有效的資料列集。|  
|DBPROP_ACCESSORDER|R/W：讀取/寫入<br /><br /> 預設值：DBPROPVAL_AO_RANDOM<br /><br /> 描述：存取順序 必須在資料列集上存取資料行的順序。<br /><br /> DBPROPVAL_AO_RANDOM：資料行可以依任何順序進行存取。<br /><br /> DBPROPVAL_AO_SEQUENTIALSTORAGEOBJECTS：當做儲存物件繫結的資料行僅能以資料行序數決定的循序順序進行存取。<br /><br /> DBPROPVAL_AO_SEQUENTIAL：所有資料行都必須以資料行序數決定的循序順序進行存取。|  
|DBPROP_APPENDONLY|這個資料列集屬性未實作的 OLE DB 驅動程式適用於 SQL Server。 嘗試讀取或寫入屬性值會產生錯誤。|  
|DBPROP_BLOCKINGSTORAGEOBJECTS|R/W：唯讀<br /><br /> 預設值：VARIANT_TRUE<br /><br /> 描述： OLE DB 驅動程式的 SQL Server 儲存物件區塊使用其他資料列集方法。|  
|DBPROP_BOOKMARKS DBPROP_LITERALBOOKMARKS|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述： SQL Server OLE DB 驅動程式支援書籤的資料列集資料列識別當 DBPROP_BOOKMARKS 或 DBPROP_LITERALBOOKMARKS 為 VARIANT_TRUE。<br /><br /> 將任一個屬性設定為 VARIANT_TRUE 不會依書籤啟用資料列集定位。 將 DBPROP_IRowsetLocate 或 DBPROP_IRowsetScroll 設定為 VARIANT_TRUE 來建立支援依書籤進行資料列集定位的資料列集。<br /><br /> SQL Server OLE DB 驅動程式會使用[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]支援包含書籤的資料列集的資料指標。 如需詳細資訊，請參閱[資料列集和 SQL Server 資料指標](../../oledb/ole-db-rowsets/rowsets-and-sql-server-cursors.md)。<br /><br /> 注意： 設定其他 OLE DB 驅動程式的 SQL Server 資料指標定義之屬性衝突的這些屬性會導致錯誤。 例如，當 DBPROP_OTHERINSERT 也為 VARIANT_TRUE 時，將 DBPROP_BOOKMARKS 設定為 VARIANT_TRUE 會在取用者嘗試開啟資料列集時產生錯誤。|  
|DBPROP_BOOKMARKSKIPPED|R/W：唯讀<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述： SQL Server OLE DB 驅動程式會傳回 DB_E_BADBOOKMARK 如果取用者無效的書籤時定位或搜尋加上書籤的資料列集。|  
|DBPROP_BOOKMARKTYPE|R/W：唯讀<br /><br /> 預設值：DBPROPVAL_BMK_NUMERIC<br /><br /> 描述： SQL Server OLE DB 驅動程式會實作數值書籤。 SQL Server 的書籤 OLE DB 驅動程式是 32 位元不帶正負號的整數，類型為 DBTYPE_UI4。|  
|DBPROP_CACHEDEFERRED|這個資料列集屬性未實作的 OLE DB 驅動程式適用於 SQL Server。 嘗試讀取或寫入屬性值會產生錯誤。|  
|DBPROP_CANFETCHBACKWARDS DBPROP_CANSCROLLBACKWARDS|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述： SQL Server 的 OLE DB 驅動程式支援反向提取和捲動非循序的資料列集中。 當 DBPROP_CANFETCHBACKWARDS 或 DBPROP_CANSCROLLBACKWARDS 為 VARIANT_TRUE 時，SQL Server OLE DB 驅動程式會建立資料指標支援的資料列集。 如需詳細資訊，請參閱[資料列集和 SQL Server 資料指標](../../oledb/ole-db-rowsets/rowsets-and-sql-server-cursors.md)。|  
|DBPROP_CANHOLDROWS|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述： 根據預設，SQL Server OLE DB 驅動程式會傳回 DB_E_ROWSNOTRELEASED 如果取用者嘗試取得多個資料列的資料列集時暫止的變更存在於目前在資料列集。 這個行為可以修改。<br /><br /> 將 DBPROP_CANHOLDROWS 和 DBPROP_IRowsetChange 同時設定為 VARIANT_TRUE 意味者加上書籤的資料列集。 如果這兩個屬性都為 VARIANT_TRUE， **IRowsetLocate**介面適用於資料列集，而且 DBPROP_BOOKMARKS 和 DBPROP_LITERALBOOKMARKS 都同時為 VARIANT_TRUE。<br /><br /> 支援 OLE DB 驅動程式的 SQL Server 資料列集包含書籤[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料指標。|  
|DBPROP_CHANGEINSERTEDROWS|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述：如果資料列集使用的是索引鍵集驅動資料指標，僅能將此屬性設定為 VARIANT_TRUE。|  
|DBPROP_COLUMNRESTRICT|R/W：唯讀<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述： SQL Server OLE DB 驅動程式將屬性設定為 VARIANT_TRUE 時無法變更資料列集中的資料行，取用者。 資料列集中的其他資料行可能可以更新，而且資料列本身可能會遭到刪除。<br /><br /> 當屬性為 VARIANT_TRUE 時，取用者會檢查*dwFlags* DBCOLUMNINFO 結構的成員，才能判斷是否可寫入個別的資料行的值。 可修改的資料行， *dwFlags*表現 DBCOLUMNFLAGS_WRITE。|  
|DBPROP_COMMANDTIMEOUT|R/W：讀取/寫入<br /><br /> 預設值： 0<br /><br /> 描述： 根據預設，SQL Server OLE DB 驅動程式不會逾時上**icommand:: Execute**方法。|  
|DBPROP_COMMITPRESERVE|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述：認可作業後的資料列集行為取決於此屬性。<br /><br /> VARIANT_TRUE: SQL Server OLE DB 驅動程式會維護有效的資料列集。<br /><br /> VARIANT_FALSE: SQL Server OLE DB 驅動程式使認可作業之後的資料列集。 資料列集物件的功能都會幾乎遺失。 它只支援**IUnknown**作業和未處理的資料列與存取子控制代碼的版本。|  
|DBPROP_DEFERRED|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述： 設定為 VARIANT_TRUE 時，OLE DB 驅動程式的 SQL Server 會嘗試使用伺服器資料指標的資料列集。 **文字**， **ntext**，和**映像**直到應用程式存取資料行不會從伺服器傳回。|  
|DBPROP_DELAYSTORAGEOBJECTS|R/W：唯讀<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述： SQL Server OLE DB 驅動程式存放區物件上支援立即更新模式。<br /><br /> 對循序資料流物件中的資料所進行之變更會立即提交至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 系統會根據資料列集交易模式認可這些修改。|  
|DBPROP_HIDDENCOLUMNS|R/W：唯讀<br /><br /> 預設值：VARIANT_FALSE<br /><br /> **描述：**隱藏資料行計數<br /><br /> 如果 DBPROP_UNIQUEROWS 為 VARIANT_TRUE，DBPROP_HIDDENCOLUMNS 屬性會傳回提供者所加入之其他「隱藏」資料行的數目，藉以唯一識別資料列集中的資料列。 這些資料行所傳回**icolumnsinfo:: Getcolumninfo**和**icolumnsrowset:: Getcolumnsrowset**。 不過，它們不包含在傳回的資料列計數*icolumnsinfo:: Getcolumninfo*所傳回的引數**icolumnsinfo:: Getcolumninfo**。<br /><br /> 若要判斷表示中的資料行總數*icolumnsinfo:: Getcolumninfo*所傳回的結構**icolumnsinfo:: Getcolumninfo**，包括隱藏的資料行，取用者會將 DBPROP_ 值要從傳回的資料行的計數 HIDDENCOLUMNS **icolumnsinfo:: Getcolumninfo**中*icolumnsinfo:: Getcolumninfo*。 如果 DBPROP_UNIQUEROWS 為 VARIANT_FALSE，DBPROP_HIDDENCOLUMNS 為零。|  
|DBPROP_IAccessor DBPROP_IColumnsInfo DBPROP_IConvertType DBPROP_IRowset DBPROP_IRowsetInfo|R/W：唯讀<br /><br /> 預設值：VARIANT_TRUE<br /><br /> 描述： SQL Server OLE DB 驅動程式支援這些介面上所有資料列集。|  
|DBPROP_IColumnsRowset|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_TRUE<br /><br /> 描述： SQL Server 的 OLE DB 驅動程式支援**IColumnsRowset**介面。|  
|DBPROP_IConnectionPointContainer|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述：IConnectionPointContainer。 如果是 VARIANT_TRUE，資料列集支援指定的介面。 如果是 VARIANT_FALSE，資料列集不支援指定的介面。 支援介面的提供者必須支援與包含 VARIANT_TRUE 值之介面相關聯的屬性。 這些屬性主要用於透過 ICommandProperties::SetProperties 來要求介面。|  
|DBPROP_IMultipleResults|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述： SQL Server 的 OLE DB 驅動程式支援**IMultipleResults**介面。|  
|DBPROP_IRowsetChange DBPROP_IRowsetUpdate|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述： SQL Server 的 OLE DB 驅動程式支援**IRowsetChange**和**IRowsetUpdate**介面。<br /><br /> 使用 DBPROP_IRowsetChange 等於 VARIANT_TRUE 建立的資料列集會表現立即更新模式行為。<br /><br /> 當 DBPROP_IRowsetUpdate 是 VARIANT_TRUE 時，DBPROP_IRowsetChange 也是 VARIANT_TRUE。 資料列集會表現延遲的更新模式行為。<br /><br /> SQL Server OLE DB 驅動程式會使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料指標支援公開的資料列集**IRowsetChange**或**IRowsetUpdate**。 如需詳細資訊，請參閱[資料列集和 SQL Server 資料指標](../../oledb/ole-db-rowsets/rowsets-and-sql-server-cursors.md)。|  
|DBPROP_IRowsetIdentity|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_TRUE<br /><br /> 描述： SQL Server 的 OLE DB 驅動程式支援**IRowsetIdentity**介面。 如果資料列集支援此介面，代表相同基礎資料列的任兩個資料列控制代碼永遠會反映相同的資料和狀態。 取用者可以呼叫**IRowsetIdentity:: IsSameRow**方法來比較兩個資料列控制代碼，以查看它們是否參考相同的資料列執行個體。|  
|DBPROP_IRowsetLocate DBPROP_IRowsetScroll|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述： SQL Server OLE DB 驅動程式可以公開**IRowsetLocate**和**IRowsetScroll**介面。<br /><br /> 當 DBPROP_IRowsetLocate 是 VARIANT_TRUE 時，DBPROP_CANFETCHBACKWARDS 和 DBPROP_CANSCROLLBACKWARDS 也是 VARIANT_TRUE。<br /><br /> 如果 DBPROP_IRowsetScroll 為 VARIANT_TRUE，DBPROP_IRowsetLocate 也為 VARIANT_TRUE，而且在資料列集上會提供這兩個介面。<br /><br /> 這兩種介面都需要書籤。 SQL Server OLE DB 驅動程式將 DBPROP_BOOKMARKS 和 DBPROP_LITERALBOOKMARKS 為 VARIANT_TRUE 時設定取用者要求任一種介面。<br /><br /> SQL Server OLE DB 驅動程式會使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料指標來支援**IRowsetLocate**和**IRowsetScroll**。 如需詳細資訊，請參閱[資料列集和 SQL Server 資料指標](../../oledb/ole-db-rowsets/rowsets-and-sql-server-cursors.md)。<br /><br /> 設定這些屬性與其他 OLE DB 驅動程式的 SQL Server 資料指標定義之屬性衝突會導致錯誤。 例如，當 DBPROP_OTHERINSERT 也為 VARIANT_TRUE 時，將 DBPROP_IRowsetScroll 設定為 VARIANT_TRUE 會在取用者嘗試開啟資料列集時產生錯誤。|  
|DBPROP_IRowsetResynch|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述： SQL Server OLE DB 驅動程式會公開**IRowsetResynch**視介面。 SQL Server OLE DB 驅動程式可以公開任何資料列集上的介面。|  
|DBPROP_ISupportErrorInfo|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_TRUE<br /><br /> 描述： SQL Server OLE DB 驅動程式會公開**ISupportErrorInfo**上資料列集介面。|  
|DBPROP_ILockBytes|OLE DB 驅動程式不會實作這個介面的 SQL Server。 嘗試讀取或寫入屬性會產生錯誤。|  
|DBPROP_ISequentialStream|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述： SQL Server OLE DB 驅動程式會公開**ISequentialStream**介面，以支援 long、 可變長度的資料儲存在[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。|  
|DBPROP_IStorage|OLE DB 驅動程式不會實作這個介面的 SQL Server。 嘗試讀取或寫入屬性會產生錯誤。|  
|DBPROP_IStream|OLE DB 驅動程式不會實作這個介面的 SQL Server。 嘗試讀取或寫入屬性會產生錯誤。|  
|DBPROP_IMMOBILEROWS|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_TRUE<br /><br /> 描述：對於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 索引鍵集資料指標，此屬性僅為 VARIANT_TRUE；對於其他所有資料指標，則為 VARIANT_FALSE。<br /><br /> VARIANT_TRUE：資料列集不會重新排列插入或更新的資料列。 如**irowsetchange:: Insertrow**，資料列會出現在資料列集結尾。 如**irowsetchange:: Setdata**，如果資料列集未經過排序，更新資料列的位置不會變更。 如果資料列集經過排序和**irowsetchange:: Setdata**變更用來排序資料列集，資料列的資料行不是移動。 如果資料列集是在一組索引鍵資料行 (通常是 DBPROP_OTHERUPDATEDELETE 為 VARIANT_TRUE，但是 DBPROP_OTHERINSERT 為 VARIANT_FALSE 的資料列集) 上建立的，變更索引鍵資料行的值通常相當於刪除目前的資料列並插入新的資料列。 因此，如果 DBPROP_OWNINSERT 為 VARIANT_FALSE，即使 DBPROP_IMMOBILEROWS 屬性為 VARIANT_TRUE，資料列可能會像是移動，或甚至從資料列集消失。<br /><br /> VARIANT_FALSE：如果資料列集經過排序，插入的資料列會以資料列集的正確順序顯示。 如果資料列集未經過排序，插入的資料列會出現在結尾。 如果**irowsetchange:: Setdata**變更資料行來移動資料列集，資料列的順序。 如果資料列集未經過排序，則不會變更資料列的位置。|  
|DBPROP_LITERALIDENTITY|R/W：唯讀<br /><br /> 預設值：VARIANT_TRUE<br /><br /> 描述：此屬性永遠是 VARIANT_TRUE。|  
|DBPROP_LOCKMODE|R/W：讀取/寫入<br /><br /> 預設值：DBPROPVAL_LM_NONE<br /><br /> 描述：資料列集 (DBPROPVAL_LM_NONE、DBPROPVAL_LM_SINGLEROW) 所執行的鎖定層級。<br /><br /> 附註： 當使用快照集隔離交易中，如果使用的索引鍵集或動態伺服器資料指標來開啟資料列集，而且鎖定模式設定為 DBPROPVAL_LM_SINGLEROW，會發生錯誤時如果其他人已自交易後更新該資料列提取資料列已啟動。 對於其他資料指標類型和鎖定模式，如果有其他人在啟動交易後更新了資料列，在使用者嘗試更新資料列前，不會發生錯誤。 在兩種情況下，伺服器會產生這些錯誤。|  
|DBPROP_MAXOPENROWS|R/W：唯讀<br /><br /> 預設值： 0<br /><br /> 描述： SQL Server OLE DB 驅動程式不會限制可在資料列集處於作用中的資料列數目。|  
|DBPROP_MAXPENDINGROWS|R/W：唯讀<br /><br /> 預設值： 0<br /><br /> 描述： SQL Server OLE DB 驅動程式不會限制變更暫止的資料列集資料列數目。|  
|DBPROP_MAXROWS|R/W：讀取/寫入<br /><br /> 預設值： 0<br /><br /> 描述： 根據預設，SQL Server OLE DB 驅動程式不會限制資料列集中的資料列數目。 當取用者設定 dbprop_maxrows 時，SQL Server OLE DB 驅動程式會使用 SET ROWCOUNT 陳述式來限制資料列集中的資料列數目。<br /><br /> SET ROWCOUNT 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 陳述式執行時，可能會造成意外的結果。 如需詳細資訊，請參閱[SET ROWCOUNT](../../../t-sql/statements/set-rowcount-transact-sql.md)。|  
|DBPROP_MAYWRITECOLUMN|這個資料列集屬性未實作的 OLE DB 驅動程式適用於 SQL Server。 嘗試讀取或寫入屬性值會產生錯誤。|  
|DBPROP_MEMORYUSAGE|這個資料列集屬性未實作的 OLE DB 驅動程式適用於 SQL Server。 嘗試讀取或寫入屬性值會產生錯誤。|  
|DBPROP_NOTIFICATIONGRANULARITY|這個資料列集屬性未實作的 OLE DB 驅動程式適用於 SQL Server。 嘗試讀取或寫入屬性值會產生錯誤。|  
|DBPROP_NOTIFICATIONPHASES|R/W：唯讀<br /><br /> 預設值： DBPROPVAL_NP_OKTODO &#124; DBPROPVAL_NP_ABOUTTODO &#124; DBPROPVAL_NP_SYNCHAFTER &#124; DBPROPVAL_NP_FAILEDTODO &#124; DBPROPVAL_NP_DIDEVENT<br /><br /> 描述： SQL Server 的 OLE DB 驅動程式支援所有告知階段。|  
|DBPROP_NOTIFYCOLUMNSET DBPROP_NOTIFYROWDELETE DBPROP_NOTIFYROWFIRSTCHANGE DBPROP_NOTIFYROWINSERT DBPROP_NOTIFYROWRESYNCH DBPROP_NOTIFYROWSETRELEASE DBPROP_NOTIFYROWSETFETCH-POSITIONCHANGE DBPROP_NOTIFYROWUNDOCHANGE DBPROP_NOTIFYROWUNDODELETE DBPROP_NOTIFYROWUNDOINSERT DBPROP_NOTIFYROWUPDATE|R/W：唯讀<br /><br /> Default: DBPROPVAL_NP_OKTODO &#124;  DBPROPVAL_NP_ABOUTTODO<br /><br /> 描述： SQL Server 告知階段，OLE DB 驅動程式會嘗試執行指定的資料列集修改前取消。 在嘗試完成之後，SQL Server OLE DB 驅動程式不支援取消階段。|  
|DBPROP_ORDEREDBOOKMARKS|這個資料列集屬性未實作的 OLE DB 驅動程式適用於 SQL Server。 嘗試讀取或寫入屬性值會產生錯誤。|  
|DBPROP_OTHERINSERT DBPROP_OTHERUPDATEDELETE DBPROP_OWNINSERT DBPROP_OWNUPDATEDELETE|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述： 設定變更可視性屬性會導致 SQL Server 以使用 OLE DB 驅動程式[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料指標來支援資料列集。 如需詳細資訊，請參閱[資料列集和 SQL Server 資料指標](../../oledb/ole-db-rowsets/rowsets-and-sql-server-cursors.md)。|  
|DBPROP_QUICKRESTART|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述： 設定為 VARIANT_TRUE 時，SQL Server OLE DB 驅動程式會嘗試使用伺服器資料指標的資料列集。|  
|DBPROP_REENTRANTEVENTS|R/W：唯讀<br /><br /> 預設值：VARIANT_TRUE<br /><br /> 描述： SQL Server 資料列集，OLE DB 驅動程式可重新進入，而且如果取用者嘗試從通知回撥存取回撥的資料列集的方法可以傳回 DB_E_NOTREENTRANT。|  
|DBPROP_REMOVEDELETED|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述： SQL Server OLE DB 驅動程式改變根據變更的可見性屬性的值[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]資料列集所公開的資料。<br /><br /> VARIANT_TRUE：重新整理資料列集時，取用者或其他 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用者刪除的資料列會從資料列集移除。 DBPROP_OTHERINSERT 為 VARIANT_TRUE。<br /><br /> VARIANT_FALSE：重新整理資料列集時，取用者或其他 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用者刪除的資料列不會從資料列集移除。 在資料列集中，已刪除之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料列的資料列狀態值為 DBROWSTATUS_E_DELETED。 DBPROP_OTHERINSERT 為 VARIANT_TRUE。<br /><br /> 此屬性僅擁有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料指標所支援的資料列集值。 如需詳細資訊，請參閱[資料列集和 SQL Server 資料指標](../../oledb/ole-db-rowsets/rowsets-and-sql-server-cursors.md)。<br /><br /> 當 DBPROP_REMOVEDELETED 屬性索引鍵集資料指標資料列集上實作時，在提取階段移除已刪除的資料列和很可能讓資料列擷取方法，例如**GetNextRows**和**GetRowsAt，**傳回 S_OK 以及比要求較少的資料列。 請注意，此行為不表示 DB_S_ENDOFROWSET 條件，而且如果有任何剩餘的資料列，所傳回的資料列數目絕不會為零。|  
|DBPROP_REPORTMULTIPLECHANGES|這個資料列集屬性未實作的 OLE DB 驅動程式適用於 SQL Server。 嘗試讀取或寫入屬性值會產生錯誤。|  
|DBPROP_RETURNPENDINGINSERTS|R/W：唯讀<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述： 呼叫提取資料列的方法時，SQL Server OLE DB 驅動程式不會傳回暫止插入資料列。|  
|DBPROP_ROWRESTRICT|R/W：唯讀<br /><br /> 預設值：VARIANT_TRUE<br /><br /> 描述： SQL Server 資料列集的 OLE DB 驅動程式不支援根據的資料列的存取權限。 如果**IRowsetChange**介面會公開資料列集， **SetData**取用者可以呼叫方法。|  
|DBPROP_ROWSET_ASYNCH|R/W：讀取/寫入<br /><br /> 預設值： 0<br /><br /> 描述：針對非同步資料列集處理提供。 此屬性位於 Rowset 屬性群組以及 DBPROPSET_ROWSET 屬性集。 類型為 VT_14。<br /><br /> SQL server OLE DB 驅動程式支援的位元遮罩中唯一的值**DBPROPVAL_ASYNCH_INITIALIZE**。|  
|DBPROP_ROWTHREADMODEL|R/W：唯讀<br /><br /> 預設值：DBPROPVAL_RT_FREETHREAD<br /><br /> 描述： SQL Server OLE DB 驅動程式支援存取其物件從單一取用者的多個執行緒。|  
|DBPROP_SERVERCURSOR|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述：設定時，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料指標用於支援資料列集。 如需詳細資訊，請參閱[資料列集和 SQL Server 資料指標](../../oledb/ole-db-rowsets/rowsets-and-sql-server-cursors.md)。|  
|DBPROP_SERVERDATAONINSERT|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述：插入的伺服器資料<br /><br /> VARIANT_TRUE：將插入傳送到伺服器時，提供者會從伺服器擷取資料來更新本機資料列快取。<br /><br /> VARIANT_FALSE：提供者不會擷取新插入之資料列的伺服器值。|  
|DBPROP_STRONGIDENTITY|R/W：唯讀<br /><br /> 預設值：VARIANT_TRUE<br /><br /> 描述：強式資料列識別。 如果資料列集上允許插入 (任一**IRowsetChange**或**IRowsetUpdate**為 true)，而且 DBPROP_UPDATABILITY 設定為支援 InsertRows，DBPROP_ 而定的值相依CHANGEINSERTEDROWS 屬性 （如果會是 VARIANT_FALSE DBPROP_CHANGEINSERTEDROWS 屬性值是 VARIANT_FALSE）。|  
|DBPROP_TRANSACTEDOBJECT|R/W：唯讀<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述： SQL Server 的 OLE DB 驅動程式支援交易的物件。 如需詳細資訊，請參閱[交易](../../oledb/ole-db-transactions/transactions.md)。|  
|DBPROP_UNIQUEROWS|R/W：讀取/寫入<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述：唯一資料列。<br /><br /> VARIANT_TRUE：每個資料列都會透過其資料行值唯一識別。 用來唯一識別資料列的資料行集中 dbcolumnflags_keycolumn 從傳回的 DBCOLUMNINFO 結構中**GetColumnInfo**方法。<br /><br /> VARIANT_FALSE：資料列可能會也可能不會透過其資料行值唯一識別。 索引鍵資料行可能會也可能不會使用 DBCOLUMNFLAGS_KEYCOLUMN 標幟。|  
|DBPROP_UPDATABILITY|R/W：讀取/寫入<br /><br /> 預設值： 0<br /><br /> 描述： SQL Server 的 OLE DB 驅動程式支援所有 DBPROP_UPDATABILITY 值。 設定 DBPROP_UPDATABILITY 並不會建立可修改的資料列集。 若要讓資料列集可以修改，設定 DBPROP_IRowsetChange 或 DBPROP_IRowsetUpdate。|  
  
 SQL Server OLE DB 驅動程式會定義提供者特有的屬性集 DBPROPSET_SQLSERVERROWSET，如本表所示。  
  
|屬性識別碼|Description|  
|-----------------|-----------------|  
|SSPROP_COLUMN_ID|資料行：ColumnID<br /><br /> R/W：唯讀<br /><br /> 類型： VT_U12 &#124; VT_ARRAY<br /><br /> 預設值：VT_EMPTY<br /><br /> 描述：在目前的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] SELECT 陳述式中，代表 COMPUTE 子句結果資料行之序數位置 (以 1 為基底) 的整數值陣列。 這是等同於 ODBC SQL_CA_SS_COLUMN_ID 屬性的 SQL Server 對等項目，OLE DB 驅動程式。|  
|SSPROP_DEFERPREPARE|資料行：否<br /><br /> R/W：讀取/寫入<br /><br /> 類型：VT_BOOL<br /><br /> 預設值：VARIANT_TRUE<br /><br /> 描述： VARIANT_TRUE： 在備妥的執行中，命令準備會延遲，直到**icommand:: Execute**稱為或執行中繼屬性作業。 如果此屬性設定為<br /><br /> VARIANT_FALSE： 陳述式時，會準備**icommandprepare:: Prepare**執行。|  
|SSPROP_IRowsetFastLoad|資料行：否<br /><br /> R/W：讀取/寫入<br /><br /> 類型：VT_BOOL<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述： 設定此屬性為 VARIANT_TRUE 以便開啟快速載入資料列集，透過**iopenrowset:: Openrowset**。 您無法設定此屬性**icommandproperties:: Setproperties**。|  
|SSPROP_ISSAsynchStatus|資料行：否。<br /><br /> R/W：讀取/寫入<br /><br /> 類型：VT_BOOL<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述： 將此屬性設定為 VARIANT_TRUE 以便使用非同步作業[ISSAsynchStatus](../../oledb/ole-db-interfaces/issasynchstatus-ole-db.md)介面。|  
|SSPROP_MAXBLOBLENGTH|資料行：否<br /><br /> R/W：讀取/寫入<br /><br /> 類型：VT_I4<br /><br /> 預設值：提供者不會限制伺服器傳回的文字大小，而且屬性值會設定為其最大值。 例如，2147483647。<br /><br /> 描述： SQL Server OLE DB 驅動程式會執行 SET TEXTSIZE 陳述式，以限制的 SELECT 陳述式所傳回的二進位大型物件 (BLOB) 資料長度。|  
|SSPROP_NOCOUNT_STATUS|資料行：NoCount<br /><br /> R/W：唯讀<br /><br /> 類型：VT_BOOL<br /><br /> 預設值：VARIANT_FALSE<br /><br /> 描述：在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中，代表 SET NOCOUNT ON/OFF 狀態的布林值：<br /><br /> VARIANT_TRUE：當 SET NOCOUNT ON 時<br /><br /> VARIANT_FALSE：當 SET NOCOUNT OFF 時|  
|SSPROP_QP_NOTIFICATION_MSGTEXT|資料行：否<br /><br /> R/W：讀取/寫入<br /><br /> 類型：VT_BSTR (允許 1-2000 個字元)<br /><br /> 預設值：空字串<br /><br /> 描述：查詢通知的訊息文字。 這是使用者定義的，而且沒有定義的格式。|  
|SSPROP_QP_NOTIFICATION_OPTIONS|資料行：否<br /><br /> R/W：讀取/寫入<br /><br /> 類型：VT_BSTR<br /><br /> 預設值：空字串<br /><br /> 描述：查詢通知選項。 這些是使用 `name=value`，在字串中指定的。 使用者負責建立此服務以及從佇列讀取通知。 查詢通知選項字串的語法為：<br /><br /> `service=<service-name>[;(local database=<database>&#124;broker instance=<broker instance>)]`<br /><br /> 例如：<br /><br /> `service=mySSBService;local database=mydb`|  
|SSPROP_QP_NOTIFICATION_TIMEOUT|資料行：否<br /><br /> R/W：讀取/寫入<br /><br /> 類型：VT_UI4<br /><br /> 預設值：432000 秒 (5 天)<br /><br /> 最小值：1 秒<br /><br /> 最大值：2^31-1 秒<br /><br /> 描述：查詢通知要維持使用中的秒數。|  
  
## <a name="see-also"></a>另請參閱  
 [資料列集](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
