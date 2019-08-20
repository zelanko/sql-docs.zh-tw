---
title: JDBC 驅動程式的備妥陳述式中繼資料快取 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 97224f53bb716abe3b79dd00df12d0eed4a63cec
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027845"
---
# <a name="prepared-statement-metadata-caching-for-the-jdbc-driver"></a>JDBC 驅動程式的備妥陳述式中繼資料快取
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

本文提供這兩項變更的相關資訊, 以強化驅動程式的效能。

## <a name="batching-of-unprepare-for-prepared-statements"></a>準備語句的 unprepare 批次處理
由於版本 6.1.6-preview, 效能的改善已透過將伺服器來回行程降至 SQL Server 來實現。 先前, 針對每個 prepareStatement 查詢, 也會傳送對 unprepare 的呼叫。 現在, 驅動程式會批次處理 unprepare 查詢, 最高可達臨界值 "ServerPreparedStatementDiscardThreshold", 其預設值為10。

> [!NOTE]  
>  使用者可以使用下列方法來變更預設值: setServerPreparedStatementDiscardThreshold (int value)

從 6.1.6-preview 引進的另一項變更是, 在此之前, 驅動程式一律會呼叫 sp_prepexec。 現在, 在第一次執行備妥的語句時, 驅動程式會呼叫 sp_executesql, 而在其餘部分會執行 sp_prepexec 並為其指派控制碼。 您可以在[這裡](https://github.com/Microsoft/mssql-jdbc/wiki/PreparedStatement-metadata-caching)找到更多詳細資料。

> [!NOTE]  
>  使用者可以使用下列方法將 enablePrepareOnFirstPreparedStatementCall 設定為**true** , 藉以將預設行為變更為先前版本的一律呼叫 Sp_prepexec: setEnablePrepareOnFirstPreparedStatementCall (布林值)

### <a name="list-of-the-new-apis-introduced-with-this-change-for-batching-of-unprepare-for-prepared-statements"></a>這項變更所引進的新 Api 清單, 適用于已備妥之語句的 unprepare 批次處理

 **SQLServerConnection**
 
|新的方法|描述|  
|-----------|-----------------|  
|int getDiscardedServerPreparedStatementCount()|傳回目前未完成的已準備語句 unprepare 動作數目。|
|void closeUnreferencedPreparedStatementHandles()|強制執行任何未處理的已捨棄備妥語句的 unprepare 要求。|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|傳回特定連接實例的行為。 如果為 false, 第一次執行呼叫 sp_executesql, 而不准備語句, 則在第二次執行時, 它會呼叫 sp_prepexec, 並實際設定備妥的語句控制碼。 下列執行會呼叫 sp_execute。 如此一來, 如果語句只執行一次, 就能減輕備妥的語句關閉 sp_unprepare 的需求。 您可以藉由呼叫 setDefaultEnablePrepareOnFirstPreparedStatementCall () 來變更這個選項的預設值。|
|void setEnablePrepareOnFirstPreparedStatementCall(boolean value)|指定特定連接實例的行為。 如果 value 為 false, 則第一次執行會呼叫 sp_executesql, 而不是準備語句, 一旦第二次執行時, 它會呼叫 sp_prepexec, 並實際設定備妥的語句控制碼。 下列執行會呼叫 sp_execute。 如此一來, 如果語句只執行一次, 就能減輕備妥的語句關閉 sp_unprepare 的需求。|
|int getServerPreparedStatementDiscardThreshold()|傳回特定連接實例的行為。 此設定可控制在執行清除伺服器上未完成的控制碼之前, 每個連接的未完成準備語句捨棄動作 (sp_unprepare)。 如果設定為 < = 1, 則會在備妥的語句關閉時立即執行 unprepare 動作。 如果設定為 {@literal >} 1, 則會將這些呼叫批次處理在一起, 以避免太常呼叫 sp_unprepare 的額外負荷。 您可以藉由呼叫 getDefaultServerPreparedStatementDiscardThreshold () 來變更這個選項的預設值。|
|void setServerPreparedStatementDiscardThreshold(int value)|指定特定連接實例的行為。 此設定可控制在執行清除伺服器上未完成的控制碼之前, 每個連接的未完成準備語句捨棄動作 (sp_unprepare)。 如果設定為 < = 1, 則會在備妥的語句關閉時立即執行 unprepare 動作。 如果設定為 > 1, 則會將這些呼叫分批放在一起, 以避免太常呼叫 sp_unprepare 的額外負荷。|

 **SQLServerDataSource**
 
|新的方法|描述|  
|-----------|-----------------|  
|void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall)|如果此設定為 false, 則第一次執行備妥的語句會呼叫 sp_executesql, 而不是準備語句, 一旦第二次執行時, 它會呼叫 sp_prepexec, 並實際設定備妥的語句控制碼。 下列執行會呼叫 sp_execute。 如此一來, 如果語句只執行一次, 就能減輕備妥的語句關閉 sp_unprepare 的需求。|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|如果此設定傳回 false, 則第一次執行備妥的語句會呼叫 sp_executesql, 而不是準備語句, 一旦第二次執行時, 它會呼叫 sp_prepexec, 並實際設定備妥的語句控制碼。 下列執行會呼叫 sp_execute。 如此一來, 如果語句只執行一次, 就能減輕備妥的語句關閉 sp_unprepare 的需求。|
|void setServerPreparedStatementDiscardThreshold (int serverPreparedStatementDiscardThreshold)|此設定可控制在執行清除伺服器上未完成的控制碼之前, 每個連接的未完成準備語句捨棄動作 (sp_unprepare)。 如果設定為 < = 1, 則會在備妥的語句關閉時立即執行 unprepare 動作。 如果設定為 {@literal >} 1, 則會將這些呼叫一起批次處理, 以避免太常呼叫 sp_unprepare 的額外負荷|
|int getServerPreparedStatementDiscardThreshold()|此設定可控制在執行清除伺服器上未完成的控制碼之前, 每個連接的未完成準備語句捨棄動作 (sp_unprepare)。 如果設定為 < = 1, 則會在備妥的語句關閉時立即執行 unprepare 動作。 如果設定為 {@literal >} 1, 則會將這些呼叫分批放在一起, 以避免太常呼叫 sp_unprepare 的額外負荷。|

## <a name="prepared-statement-metatada-caching"></a>備妥的語句關於快取
從 6.3.0-preview 版本開始, Microsoft JDBC driver for SQL Server 支援備妥的語句快取。 在 v 6.3.0-preview 之前, 如果有一個查詢已準備好並儲存在快取中, 則再次呼叫相同的查詢並不會產生準備。 現在, 驅動程式會查閱快取中的查詢, 並尋找控制碼, 並使用 sp_execute 來執行它。
預設會**停用**備妥的語句中繼資料快取。 若要啟用它, 您必須在連線物件上呼叫下列方法:

`setStatementPoolingCacheSize(int value)   //value is the desired cache size (any value bigger than 0)`
`setDisableStatementPooling(boolean value) //false allows the caching to take place`

例如：`connection.setStatementPoolingCacheSize(10)`
`connection.setDisableStatementPooling(false)`

### <a name="list-of-the-new-apis-introduced-with-this-change-for-prepared-statement-metadata-caching"></a>此變更所引進的新 Api 清單, 適用于備妥的語句中繼資料快取

 **SQLServerConnection**
 
|新的方法|描述|  
|-----------|-----------------|  
|void setDisableStatementPooling (布林值)|將語句集區設定為 true 或 false。|
|boolean getDisableStatementPooling()|如果停用語句集區, 則傳回 true。|
|void setStatementPoolingCacheSize(int value)|指定此連接的已備妥語句快取大小。 小於1的值表示沒有快取。|
|int getStatementPoolingCacheSize()|傳回此連接備妥之語句快取的大小。 小於1的值表示沒有快取。|
|int getStatementHandleCacheEntryCount()|傳回目前已準備好的已共用語句控制碼數目。|
|boolean isPreparedStatementCachingEnabled()|此連接是否已啟用語句集區。|

 **SQLServerDataSource**
 
|新的方法|描述|  
|-----------|-----------------|  
|void setDisableStatementPooling (布林值 disableStatementPooling)|將語句集區設定為 true 或 false|
|boolean getDisableStatementPooling()|如果停用語句集區, 則傳回 true。|
|void setStatementPoolingCacheSize(int statementPoolingCacheSize)|指定此連接的已備妥語句快取大小。 小於1的值表示沒有快取。|
|int getStatementPoolingCacheSize()|傳回此連接備妥之語句快取的大小。 小於1的值表示沒有快取。|

## <a name="see-also"></a>另請參閱  
 [改善JDBC 驅動程式的效能與可靠性](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
