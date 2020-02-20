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
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "69027845"
---
# <a name="prepared-statement-metadata-caching-for-the-jdbc-driver"></a>JDBC 驅動程式的備妥陳述式中繼資料快取
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

此文章提供這兩個變更的相關資訊，實作之後可強化驅動程式的效能。

## <a name="batching-of-unprepare-for-prepared-statements"></a>備妥陳述式的未準備批次處理
從 6.1.6-preview 版開始，效能的改善已透過將伺服器來回行程降至 SQL Server 來實作。 先前，針對每個 prepareStatement 查詢，也會傳送對 unprepare 的呼叫。 現在，驅動程式會批次處理 unprepare 查詢，最高可達閾值 "ServerPreparedStatementDiscardThreshold"，其預設值為 10。

> [!NOTE]  
>  使用者可以使用下列方法變更預設值：setServerPreparedStatementDiscardThreshold(int value)

從 6.1.6-preview 引入的另一項變更是，在此之前，驅動程式一律會呼叫 sp_prepexec。 現在，在第一次執行備妥的陳述式時，驅動程式會呼叫 sp_executesql，而在之後則會執行 sp_prepexec 並為其指派一個控制代碼。 在 [這裡](https://github.com/Microsoft/mssql-jdbc/wiki/PreparedStatement-metadata-caching)可以找到更多詳細資訊。

> [!NOTE]  
>  使用者可以使用下列方法，將 enablePrepareOnFirstPreparedStatementCall 設定為 **true**，以便將預設行為變更為舊版的一律呼叫 sp_prepexec：setEnablePrepareOnFirstPreparedStatementCall(boolean value)

### <a name="list-of-the-new-apis-introduced-with-this-change-for-batching-of-unprepare-for-prepared-statements"></a>與這項變更一起引入之新 API 的清單，適用於備妥陳述式的未準備批次處理

 **SQLServerConnection**
 
|新的方法|描述|  
|-----------|-----------------|  
|int getDiscardedServerPreparedStatementCount()|傳回目前未完成備妥陳述式未準備動作的數目。|
|void closeUnreferencedPreparedStatementHandles()|強制執行任何未完成捨棄備妥陳述式的未準備要求。|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|傳回特定連線執行個體的行為。 如果為 false，則第一次執行將會呼叫 sp_executesql 而不是備妥陳述式，一旦第二次執行時，就會呼叫 sp_prepexec 並實際設定備妥陳述式控制代碼。 下列執行會呼叫 sp_execute。 如果該陳述式僅執行一次，則無需在備妥陳述式結束時使用 sp_unprepare。 您可以藉由呼叫 setDefaultEnablePrepareOnFirstPreparedStatementCall() 來變更這個選項的預設值。|
|void setEnablePrepareOnFirstPreparedStatementCall(boolean value)|指定特定連線執行個體的行為。 如果值為 false，則第一次執行將會呼叫 sp_executesql 而不是備妥陳述式，一旦第二次執行時，就會呼叫 sp_prepexec 並實際設定備妥陳述式控制代碼。 下列執行會呼叫 sp_execute。 如果該陳述式僅執行一次，則無需在備妥陳述式結束時使用 sp_unprepare。|
|int getServerPreparedStatementDiscardThreshold()|傳回特定連線執行個體的行為。 此設定可控制在執行清理伺服器上未完成控制代碼的呼叫之前，每個連線可以有多少個未完成的備妥陳述式捨棄動作 (sp_unprepare) 尚未完成。 如果設定為 <= 1，就會在備妥陳述式一結束時，立即執行取消準備動作。 如果將其設定為 {@literal >} 1，則會將這些呼叫批次處理在一起，以避免太常呼叫 sp_unprepare 所造成的額外負荷。 您可以藉由呼叫 getDefaultServerPreparedStatementDiscardThreshold() 來變更這個選項的預設值。|
|void setServerPreparedStatementDiscardThreshold(int value)|指定特定連線執行個體的行為。 此設定可控制在執行清理伺服器上未完成控制代碼的呼叫之前，每個連線可以有多少個未完成的備妥陳述式捨棄動作 (sp_unprepare) 尚未完成。 如果設定為 <= 1，就會在備妥陳述式一結束時，立即執行取消準備動作。 如果將其設定為 > 1，則會將這些呼叫批次處理在一起，以避免太常呼叫 sp_unprepare 所造成的額外負荷。|

 **SQLServerDataSource**
 
|新的方法|描述|  
|-----------|-----------------|  
|void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall)|如果此設定為 false，則第一次執行備妥陳述式會呼叫 sp_executesql 而不是備妥陳述式，一旦第二次執行時，就會呼叫 sp_prepexec 並實際設定備妥陳述式控制代碼。 下列執行會呼叫 sp_execute。 如果該陳述式僅執行一次，則無需在備妥陳述式結束時使用 sp_unprepare。|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|如果此設定傳回 false，則第一次執行備妥陳述式會呼叫 sp_executesql 而不是備妥陳述式，一旦第二次執行時，就會呼叫 sp_prepexec 並實際設定備妥陳述式控制代碼。 下列執行會呼叫 sp_execute。 如果該陳述式僅執行一次，則無需在備妥陳述式結束時使用 sp_unprepare。|
|void setServerPreparedStatementDiscardThreshold(int serverPreparedStatementDiscardThreshold)|此設定可控制在執行清理伺服器上未完成控制代碼的呼叫之前，每個連線可以有多少個未完成的備妥陳述式捨棄動作 (sp_unprepare) 尚未完成。 如果設定為 <= 1，就會在備妥陳述式一結束時，立即執行取消準備動作。 如果將其設定為 {@literal >} 1，則會將這些呼叫批次處理在一起，以避免太常呼叫 sp_unprepare 所造成的額外負荷|
|int getServerPreparedStatementDiscardThreshold()|此設定可控制在執行清理伺服器上未完成控制代碼的呼叫之前，每個連線可以有多少個未完成的備妥陳述式捨棄動作 (sp_unprepare) 尚未完成。 如果設定為 <= 1，就會在備妥陳述式一結束時，立即執行取消準備動作。 如果將其設定為 {@literal >} 1，則會將這些呼叫批次處理在一起，以避免太常呼叫 sp_unprepare 所造成的額外負荷。|

## <a name="prepared-statement-metatada-caching"></a>備妥陳述式中繼資料快取
從 6.3.0-preview 版開始，Microsoft JDBC Driver for SQL Server 支援備妥陳述式快取。 在 v 6.3.0-preview 之前，如果有人執行已經備妥並儲存在快取中的查詢，則再次呼叫相同的查詢並不會導致準備該查詢。 現在，驅動程式會查閱快取中的查詢，並尋找控制代碼，然後使用 sp_execute 加以執行。
備妥陳述式中繼資料快取預設為**停用**狀態。 若要啟用該快取，您必須針對連線物件呼叫下列方法：

`setStatementPoolingCacheSize(int value)   //value is the desired cache size (any value bigger than 0)`
`setDisableStatementPooling(boolean value) //false allows the caching to take place`

例如：`connection.setStatementPoolingCacheSize(10)`
`connection.setDisableStatementPooling(false)`

### <a name="list-of-the-new-apis-introduced-with-this-change-for-prepared-statement-metadata-caching"></a>與這項變更一起引入之新 API 的清單，適用於備妥陳述式中繼資料快取

 **SQLServerConnection**
 
|新的方法|描述|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean value)|將陳述式共用設定為 true 或 false。|
|boolean getDisableStatementPooling()|如果陳述式共用遭到停用，則傳回 true。|
|void setStatementPoolingCacheSize(int value)|指定此連線之備妥陳述式快取的大小。 小於 1 的值表示沒有快取。|
|int getStatementPoolingCacheSize()|傳回此連線之備妥陳述式快取的大小。 小於 1 的值表示沒有快取。|
|int getStatementHandleCacheEntryCount()|傳回目前共用備妥陳述式控制代碼的數目。|
|boolean isPreparedStatementCachingEnabled()|無論陳述式共用是否已針對此連線啟用。|

 **SQLServerDataSource**
 
|新的方法|描述|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean disableStatementPooling)|將陳述式共用設定為 true 或 false|
|boolean getDisableStatementPooling()|如果陳述式共用遭到停用，則傳回 true。|
|void setStatementPoolingCacheSize(int statementPoolingCacheSize)|指定此連線之備妥陳述式快取的大小。 小於 1 的值表示沒有快取。|
|int getStatementPoolingCacheSize()|傳回此連線之備妥陳述式快取的大小。 小於 1 的值表示沒有快取。|

## <a name="see-also"></a>另請參閱  
 [改善JDBC 驅動程式的效能與可靠性](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
