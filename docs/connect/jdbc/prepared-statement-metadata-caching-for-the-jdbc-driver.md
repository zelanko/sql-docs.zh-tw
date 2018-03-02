---
title: "備妥的陳述式中繼資料，JDBC 驅動程式的快取 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 13d4c0766552d9472038ffe7f2ff7fed6d73584d
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/02/2018
---
# <a name="prepared-statement-metadata-caching-for-the-jdbc-driver"></a>JDBC 驅動程式的快取的已備妥的陳述式中繼資料
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

這篇文章提供兩種實作來增強的驅動程式效能的變更資訊。

## <a name="batching-of-unprepare-for-prepared-statements"></a>批次進行取消準備備妥的陳述式
因為版本 6.1.6-preview，效能改善實作透過最小化伺服器往返到 SQL Server。 先前，針對每個 prepareStatement 查詢中，取消準備的呼叫也會傳送。 現在，驅動程式會批次處理 unprepare 查詢最多的臨界值 」 ServerPreparedStatementDiscardThreshold"，其預設值為 10。

> [!NOTE]  
>  使用者可以使用下列方法變更預設值： setServerPreparedStatementDiscardThreshold （int 值）

從 6.1.6-preview 導入的一項多個變更是在此之前，驅動程式會一律呼叫 sp_prepexec。 現在，針對第一個執行已備妥的陳述式時，驅動程式會呼叫 sp_executesql，其餘它會執行 sp_prepexec 並指派給它的控制代碼。 可以找到更多詳細資料[這裡](https://github.com/Microsoft/mssql-jdbc/wiki/PreparedStatement-metadata-caching)。

> [!NOTE]  
>  使用者可以變更預設行為與舊版一律呼叫設定 enablePrepareOnFirstPreparedStatementCall 至 sp_prepexec **true**使用下列方法：setEnablePrepareOnFirstPreparedStatementCall （布林值）

### <a name="list-of-the-new-apis-introduced-with-this-change-for-batching-of-unprepare-for-prepared-statements"></a>所導入的這項變更，進行批次處理的新 Api 清單取消準備備妥的陳述式

 **SQLServerConnection**
 
|新的方法|Description|  
|-----------|-----------------|  
|int getDiscardedServerPreparedStatementCount()|傳回的目前未完成已備妥陳述式取消準備動作。|
|void closeUnreferencedPreparedStatementHandles()|強制 unprepare 要求的任何未完成捨棄備妥陳述式來執行。|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|傳回特定的連接執行個體的行為。 如果為 false 第一次執行 sp_executesql 不準備的陳述式，它會呼叫 sp_prepexec 會發生的第二次執行之後和實際設定的已備妥的陳述式控制代碼。 下列執行呼叫 sp_execute。 這減輕 sp_unprepare 備妥的陳述式需要關閉如果陳述式只執行一次。 呼叫 setDefaultEnablePrepareOnFirstPreparedStatementCall() 可以變更這個選項的預設值。|
|void setEnablePrepareOnFirstPreparedStatementCall(boolean value)|指定特定的連接執行個體的行為。 如果值為 false 第一次執行 sp_executesql 不準備的陳述式，它會呼叫 sp_prepexec 會發生的第二次執行之後和實際設定的已備妥的陳述式控制代碼。 下列執行呼叫 sp_execute。 這減輕 sp_unprepare 備妥的陳述式需要關閉如果陳述式只執行一次。|
|int getServerPreparedStatementDiscardThreshold()|傳回特定的連接執行個體的行為。 此設定會控制多少未完成備妥的陳述式捨棄之前呼叫，以清除伺服器上未處理的控制代碼將會執行動作 (sp_unprepare) 可以是未處理的每個連接。 如果設定為 < = 1，取消準備備妥的陳述式關閉上立即執行動作。 如果設為 {@literal >} 1，這些呼叫會批次處理以避免呼叫 sp_unprepare 的額外負荷太過頻繁。 呼叫 getDefaultServerPreparedStatementDiscardThreshold() 可以變更這個選項的預設值。|
|void setServerPreparedStatementDiscardThreshold(int value)|指定特定的連接執行個體的行為。 此設定會控制多少未完成備妥的陳述式捨棄之前呼叫，以清除伺服器上未處理的控制代碼將會執行動作 (sp_unprepare) 可以是未處理的每個連接。 如果設定為 < = 1 unprepare 動作會立即關閉已備妥的陳述式上執行。 如果設定為 > 1 這些呼叫會一起批次處理以避免太過頻繁呼叫 sp_unprepare 的額外負荷。|

 **SQLServerDataSource**
 
|新的方法|Description|  
|-----------|-----------------|  
|void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall)|如果此設定為 false 的已備妥的陳述式的第一次執行 sp_executesql 不準備的陳述式，它會呼叫 sp_prepexec 會發生的第二次執行之後和實際安裝的已備妥的陳述式控制代碼。 下列執行呼叫 sp_execute。 這減輕 sp_unprepare 備妥的陳述式需要關閉如果陳述式只執行一次。|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|如果此設定會傳回 false 備妥的陳述式的第一次執行 sp_executesql，而且一旦發生第二次執行準備陳述式，它會呼叫 sp_prepexec，而實際安裝的已備妥的陳述式控制代碼。 下列執行呼叫 sp_execute。 這減輕 sp_unprepare 備妥的陳述式需要關閉如果陳述式只執行一次。|
|void setServerPreparedStatementDiscardThreshold(int serverPreparedStatementDiscardThreshold)|此設定會控制多少未完成備妥的陳述式捨棄之前呼叫，以清除伺服器上未處理的控制代碼將會執行動作 (sp_unprepare) 可以是未處理的每個連接。 如果設定為 < = 1 unprepare 動作會立即關閉已備妥的陳述式上執行。 如果設為 {@literal >} 1 這些呼叫會一起批次處理，以避免太過頻繁呼叫 sp_unprepare 的額外負荷|
|int getServerPreparedStatementDiscardThreshold()|此設定會控制多少未完成備妥的陳述式捨棄之前呼叫，以清除伺服器上未處理的控制代碼將會執行動作 (sp_unprepare) 可以是未處理的每個連接。 如果設定為 < = 1 unprepare 動作會立即關閉已備妥的陳述式上執行。 如果設為 {@literal >} 1 這些呼叫會一起批次處理，以避免太過頻繁呼叫 sp_unprepare 的額外負荷。|

## <a name="prepared-statement-metatada-caching"></a>已備妥的陳述式中繼資料快取
6.3.0-preview 版 Microsoft JDBC driver for SQL Server 支援已備妥的陳述式快取。 之前 v6.3.0 預覽，如果其中一個執行的查詢，已備妥並儲存在快取中，已再次呼叫相同的查詢不會導致準備。 現在，驅動程式查閱快取中的查詢尋找的控制代碼和 sp_execute 來執行。
已備妥的陳述式中繼資料快取是**停用**預設。 若要啟用它，您需要的連接物件上呼叫下列方法：

`setStatementPoolingCacheSize(int value)   //value is the desired cache size (any value bigger than 0)`
`setDisableStatementPooling(boolean value) //false allows the caching to take place`

例如： `connection.setStatementPoolingCacheSize(10)`
`connection.setDisableStatementPooling(false)`

### <a name="list-of-the-new-apis-introduced-with-this-change-for-prepared-statement-metadata-caching"></a>這項變更，已備妥的陳述式所引進的新 api 清單中繼資料快取

 **SQLServerConnection**
 
|新的方法|Description|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean value)|設定為 true 或 false 的陳述式集區。|
|boolean getDisableStatementPooling()|如果陳述式共用已停用，則傳回 true。|
|void setStatementPoolingCacheSize(int value)|指定此連線的已備妥的陳述式快取大小。 小於 1 的值表示無快取。|
|int getStatementPoolingCacheSize()|傳回此連線的已備妥的陳述式快取大小。 小於 1 的值表示無快取。|
|int getStatementHandleCacheEntryCount()|傳回目前的集區已備妥的陳述式控制代碼數目。|
|boolean isPreparedStatementCachingEnabled()|是否已啟用共用陳述式或不適用於此連線。|

 **SQLServerDataSource**
 
|新的方法|Description|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean disableStatementPooling)|設定共用的陳述式，為 true 或 false|
|boolean getDisableStatementPooling()|如果陳述式共用已停用，則傳回 true。|
|void setStatementPoolingCacheSize(int statementPoolingCacheSize)|指定此連線的已備妥的陳述式快取大小。 小於 1 的值表示無快取。|
|int getStatementPoolingCacheSize()|傳回此連線的已備妥的陳述式快取大小。 小於 1 的值表示無快取。|

## <a name="see-also"></a>另請參閱  
 [善 JDBC Driver 的效能與可靠性](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
