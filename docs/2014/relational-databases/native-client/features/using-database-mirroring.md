---
title: 使用資料庫鏡像 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- SQL Server Native Client, database mirroring
- data access [SQL Server Native Client], database mirroring
- database mirroring [SQL Server], connecting clients to
- SQLNCLI, database mirroring
- SQL Server Native Client ODBC driver, database mirroring
- SQL Server Native Client OLE DB provider, database mirroring
ms.assetid: 71b15712-7972-4465-9274-e0ddc271eedc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5d7db93bdbe00b6aa1bc2525c0e8ed47e45aaf15
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63225333"
---
# <a name="using-database-mirroring"></a>使用資料庫鏡像
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)] 請改用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]。  
  
 在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中導入的資料庫鏡像是一套增加資料庫可用性與資料冗餘的方案。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 原生用戶端提供對資料庫鏡像，隱含支援，因此開發人員不需要撰寫任何程式碼或採取其他任何動作，設定資料庫之後。  
  
 資料庫鏡像是根據每一個資料庫來實作，它會在待命伺服器上保留 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 生產資料庫的複本。 此伺服器為熱或暖待命伺服器，端視資料庫鏡像工作階段的組態和狀態而定。 熱待命伺服器支援不會遺失任何已認可交易的快速容錯移轉，而暖待命伺服器支援強制服務 (資料可能會遺失)。  
  
 生產資料庫稱為「主體資料庫」  ，而待命副本則稱為「鏡像資料庫」  。 主體資料庫和鏡像資料庫必須位於個別的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體 (伺服器執行個體) 上，如有可能，也應該位於個別的電腦上。  
  
 稱為「主體伺服器」  的實際執行伺服器執行個體會與稱為「鏡像伺服器」  的待命伺服器執行個體進行通訊。 主體伺服器和鏡像伺服器會在資料庫鏡像「工作階段」  內當做夥伴運作。 如果主體伺服器失敗，則鏡像伺服器可以透過稱為「容錯移轉」  的處理序，使鏡像伺服器的資料庫成為主體資料庫。 例如，Partner_A 與 Partner_B 是兩個夥伴伺服器，其中主體資料庫一開始位於 Partner_A 上做為主體伺服器，而鏡像資料庫位於 Partner_B 上做為鏡像伺服器。 如果 Partner_A 離線，Partner_B 上的資料庫可以容錯移轉，變成目前的主體資料庫。 當 Partner_A 重新加入鏡像工作階段時，它會變成鏡像伺服器而其資料庫會變成鏡像資料庫。  
  
 替代的資料庫鏡像組態提供不同層次的效能及資料安全，並支援不同形式的容錯移轉。 如需詳細資訊，請參閱[資料庫鏡像 &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-sql-server.md)。  
  
 指定鏡像資料庫名稱時，可以使用別名。  
  
> [!NOTE]  
>  初始連接嘗試與鏡像資料庫的重新連線嘗試的相關資訊，請參閱[用戶端連接至資料庫鏡像工作階段&#40;SQL Server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)。  
  
## <a name="programming-considerations"></a>程式設計考量  
 當主體資料庫伺服器失敗時，用戶端應用程式會在回應 API 呼叫時收到錯誤，這表示與資料庫的連接已經中斷。 發生這個情況時，對於資料庫的任何未認可變更都會遺失，而且目前的交易會回復。 如果發生這個情況，應用程式應該關閉連接 (或釋出資料來源物件) 然後再重新開啟它。 此連接會以透明的方式重新導向鏡像資料庫，現在當做主體伺服器使用。  
  
 建立連接時，主體伺服器會將其容錯移轉夥伴的識別傳送到容錯移轉發生時所使用的用戶端。 在應用程式嘗試在主體伺服器失敗後建立連接的情況下，用戶端不會知道容錯移轉夥伴的識別。 為了讓用戶端有機會處理此狀況，初始化屬性和相關聯的連接字串關鍵字可讓用戶端自行指定容錯移轉夥伴的識別。 只有在有可用的主體伺服器，但未使用時，才會在此狀況中使用用戶端屬性。 如果用戶端提供的容錯移轉夥伴伺服器指的不是當做容錯移轉夥伴的伺服器，伺服器就會拒絕連接。 若要讓應用程式符合組態變更，實際容錯移轉夥伴的識別可以透過檢查建立連接後的屬性來判斷。 如果第一次建立連接的嘗試失敗，您應該考慮快取處理夥伴資訊來更新連接字串或想出重試策略。  
  
> [!NOTE]  
>  如果您要在 DSN、連接字串或連接屬性 (Property)/屬性 (Attribute) 中使用此功能，您必須明確指定連接所使用的資料庫。 如果未完成此動作，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 將不會嘗試容錯移轉到夥伴資料庫。  
>   
>  鏡像是資料庫的一個功能。 使用多個資料庫的應用程式可能無法使用此功能。  
>   
>  此外，伺服器名稱不區分大小寫，但是資料庫名稱會區分大小寫。 因此，您應該確認您在 DSN 和連接字串中使用相同的大小寫。  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB 提供者  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者透過支援資料庫鏡像連接和連接字串屬性。 SSPROP_INIT_FAILOVERPARTNER 屬性已加入到 DBPROPSET_SQLSERVERDBINIT 屬性集，而 `FailoverPartner` 關鍵字是 DBPROP_INIT_PROVIDERSTRING 的新連接字串屬性。 如需詳細資訊，請參閱 <<c0> [ 搭配 SQL Server Native Client 使用連接字串關鍵字](../applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 容錯移轉快取會維護，只要載入提供者，直到**CoUninitialize**呼叫或只要應用程式有管理之特定物件的參考[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者，例如資料來源物件。  
  
 如需詳細資訊[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供者支援資料庫鏡像，請參閱[初始化和授權屬性](../../native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)。  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC 驅動程式  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驅動程式支援資料庫鏡像透過連接和連接字串屬性。 具體來說，已用於加入 SQL_COPT_SS_FAILOVER_PARTNER 屬性[SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md)並[SQLGetConnectAttr](../../native-client-odbc-api/sqlgetconnectattr.md)函式，而`Failover_Partner`關鍵字已新增為新的連接字串屬性。  
  
 只要應用程式至少有配置一個環境控制代碼，就可以維持容錯移轉快取。 相反地，取消配置最後一個環境控制代碼時，容錯移轉快取就會遺失。  
  
> [!NOTE]  
>  ODBC 驅動程式管理員已經增強，可以支援容錯移轉伺服器名稱的規格。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 功能](sql-server-native-client-features.md)   
 [將用戶端連接至資料庫鏡像工作階段 &#40;SQL Server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)   
 [資料庫鏡像 &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
