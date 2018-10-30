---
title: JDBC 驅動程式的備妥陳述式中繼資料快取 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3c412a4364e18a70cf10d9896138c5056318ae20
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47767336"
---
# <a name="prepared-statement-metadata-caching-for-the-jdbc-driver"></a>JDBC Driver 的備妥陳述式中繼資料快取
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

本文章提供實作以增強的驅動程式效能的兩個變更的資訊。

## <a name="batching-of-unprepare-for-prepared-statements"></a>批次進行取消準備備妥的陳述式
因為版本 6.1.6-preview，效能改善已實作透過最小化的伺服器往返到 SQL Server。 先前，針對每個 prepareStatement 查詢中，取消準備的呼叫也會傳送。 現在，驅動程式批次 unprepare 查詢最多的臨界值 」 ServerPreparedStatementDiscardThreshold"，其預設值為 10。

> [!NOTE]  
>  使用者可以變更預設值，使用下列方法： setServerPreparedStatementDiscardThreshold （int 值）

從 6.1.6-preview 引進一項變更是在此之前，驅動程式會一律呼叫 sp_prepexec。 現在，第一個執行已備妥的陳述式時，驅動程式會呼叫 sp_executesql 以及其餘部分方法，它可以執行 sp_prepexec，並指派給它的控制代碼。 可以找到更多詳細資料[此處](https://github.com/Microsoft/mssql-jdbc/wiki/PreparedStatement-metadata-caching)。

> [!NOTE]  
>  使用者可以變更預設行為，舊版一律呼叫來設定的 enablePrepareOnFirstPreparedStatementCall sp_prepexec **，則為 true**使用下列方法：setEnablePrepareOnFirstPreparedStatementCall （布林值）

### <a name="list-of-the-new-apis-introduced-with-this-change-for-batching-of-unprepare-for-prepared-statements"></a>透過這項變更進行批次處理的引進的新 Api 清單取消準備備妥的陳述式

 **SQLServerConnection**
 
|新的方法|Description|  
|-----------|-----------------|  
|int getDiscardedServerPreparedStatementCount()|傳回的目前未完成已備妥之陳述式取消準備動作。|
|void closeUnreferencedPreparedStatementHandles()|強制執行任何未處理捨棄已備妥要執行陳述式的 unprepare 要求。|
|布林 getEnablePrepareOnFirstPreparedStatementCall()|傳回特定的連接執行個體的行為。 如果為 false 第一次執行呼叫 sp_executesql 後第二次執行發生呼叫 sp_prepexec 準備陳述式，並實際設定備妥的陳述式控制代碼。 下列執行呼叫 sp_execute。 這減輕 sp_unprepare 備妥的陳述式需要關閉如果陳述式只執行一次。 呼叫 setDefaultEnablePrepareOnFirstPreparedStatementCall() 可以變更這個選項的預設值。|
|void setEnablePrepareOnFirstPreparedStatementCall(boolean value)|指定特定的連接執行個體的行為。 如果值為 false 第一次執行呼叫 sp_executesql 後第二次執行發生呼叫 sp_prepexec 準備陳述式和實際設定備妥的陳述式控制代碼。 下列執行呼叫 sp_execute。 這減輕 sp_unprepare 備妥的陳述式需要關閉如果陳述式只執行一次。|
|int getServerPreparedStatementDiscardThreshold()|傳回特定的連接執行個體的行為。 此設定會控制多少未完成已備妥陳述式捨棄動作 (sp_unprepare) 可以是未處理的每個連接，呼叫以清除 在伺服器上未處理的控制代碼會在執行之前。 如果設定為 < = 1，unprepare 關閉已備妥的陳述式會立即執行動作。 如果設定為 {@literal >} 1，這些呼叫一個批次，以避免太頻繁的呼叫 sp_unprepare 的額外負荷。 呼叫 getDefaultServerPreparedStatementDiscardThreshold() 可以變更這個選項的預設值。|
|void setServerPreparedStatementDiscardThreshold(int value)|指定特定的連接執行個體的行為。 此設定會控制多少未完成已備妥陳述式捨棄動作 (sp_unprepare) 可以是未處理的每個連接，呼叫以清除 在伺服器上未處理的控制代碼會在執行之前。 如果設定為 < = 1 unprepare 動作會立即關閉已備妥的陳述式上執行。 如果設為 > 1 時這些呼叫被批次，以避免太頻繁呼叫 sp_unprepare 的額外負荷。|

 **SQLServerDataSource**
 
|新的方法|Description|  
|-----------|-----------------|  
|void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall)|如果此設定為 false 備妥的陳述式的第一次執行呼叫 sp_executesql 後第二次執行發生呼叫 sp_prepexec 準備陳述式，和實際設定備妥的陳述式控制代碼。 下列執行呼叫 sp_execute。 這減輕 sp_unprepare 備妥的陳述式需要關閉如果陳述式只執行一次。|
|布林 getEnablePrepareOnFirstPreparedStatementCall()|如果此設定會傳回 false 的已備妥的陳述式的第一次執行 sp_executesql，一旦發生第二次執行準備陳述式，它會呼叫 sp_prepexec，並實際設定備妥的陳述式控制代碼。 下列執行呼叫 sp_execute。 這減輕 sp_unprepare 備妥的陳述式需要關閉如果陳述式只執行一次。|
|void setServerPreparedStatementDiscardThreshold(int serverPreparedStatementDiscardThreshold)|此設定會控制多少未完成已備妥陳述式捨棄動作 (sp_unprepare) 可以是未處理的每個連接，呼叫以清除 在伺服器上未處理的控制代碼會在執行之前。 如果設定為 < = 1 unprepare 動作會立即關閉已備妥的陳述式上執行。 如果設定為 {@literal >} 1 這些呼叫會一起批次處理，以避免太頻繁呼叫 sp_unprepare 的額外負荷|
|int getServerPreparedStatementDiscardThreshold()|此設定會控制多少未完成已備妥陳述式捨棄動作 (sp_unprepare) 可以是未處理的每個連接，呼叫以清除 在伺服器上未處理的控制代碼會在執行之前。 如果設定為 < = 1 unprepare 動作會立即關閉已備妥的陳述式上執行。 如果設定為 {@literal >} 1 這些呼叫會一起批次處理，以避免太頻繁呼叫 sp_unprepare 的額外負荷。|

## <a name="prepared-statement-metatada-caching"></a>備妥的陳述式中繼資料快取
從 6.3.0-preview 版開始，Microsoft JDBC driver for SQL Server 支援已備妥的陳述式快取。 之前 v6.3.0-preview，如果其中一個執行的查詢，已備妥並儲存在快取中，已再次呼叫相同的查詢不會準備。 現在，驅動程式查閱快取中的查詢尋找的控制代碼和 sp_execute 來執行。
備妥的陳述式中繼資料快取**停用**預設。 若要啟用它，您需要在連線物件上呼叫下列方法：

`setStatementPoolingCacheSize(int value)   //value is the desired cache size (any value bigger than 0)`
`setDisableStatementPooling(boolean value) //false allows the caching to take place`

例如：`connection.setStatementPoolingCacheSize(10)`
`connection.setDisableStatementPooling(false)`

### <a name="list-of-the-new-apis-introduced-with-this-change-for-prepared-statement-metadata-caching"></a>透過這項變更，已備妥的陳述式中引進的新 Api 清單中繼資料快取

 **SQLServerConnection**
 
|新的方法|Description|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean value)|設定為 true 或 false 的陳述式共用。|
|布林 getDisableStatementPooling()|如果陳述式共用已停用，則傳回 true。|
|void setStatementPoolingCacheSize(int value)|指定此連線的已備妥的陳述式快取的大小。 小於 1 的值表示沒有快取。|
|int getStatementPoolingCacheSize()|傳回此連線的已備妥的陳述式快取的大小。 小於 1 的值表示沒有快取。|
|int getStatementHandleCacheEntryCount()|傳回目前的集區的已備妥之陳述式控制代碼數目。|
|布林 isPreparedStatementCachingEnabled()|是否啟用陳述式共用或不適用於此連線。|

 **SQLServerDataSource**
 
|新的方法|Description|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean disableStatementPooling)|設定共用的陳述式，為 true 或 false|
|布林 getDisableStatementPooling()|如果陳述式共用已停用，則傳回 true。|
|void setStatementPoolingCacheSize(int statementPoolingCacheSize)|指定此連線的已備妥的陳述式快取的大小。 小於 1 的值表示沒有快取。|
|int getStatementPoolingCacheSize()|傳回此連線的已備妥的陳述式快取的大小。 小於 1 的值表示沒有快取。|

## <a name="see-also"></a>另請參閱  
 [善 JDBC Driver 的效能與可靠性](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
