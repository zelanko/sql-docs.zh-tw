---
title: 使用資料庫鏡像 |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5c2db9621490f4dc718516e5829f6704b20ee0e9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "73761329"
---
# <a name="using-database-mirroring"></a>使用資料庫鏡像
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)] 請改用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]。  
  
 在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中導入的資料庫鏡像是一套增加資料庫可用性與資料冗餘的方案。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client 會提供對資料庫鏡像的隱含支援，因此，開發人員在針對資料庫設定之後，不需要撰寫任何程式碼或採取任何其他動作。  
  
 資料庫鏡像是根據每一個資料庫來實作，它會在待命伺服器上保留 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 生產資料庫的複本。 此伺服器為熱或暖待命伺服器，端視資料庫鏡像工作階段的組態和狀態而定。 熱待命伺服器支援不會遺失任何已認可交易的快速容錯移轉，而暖待命伺服器支援強制服務 (資料可能會遺失)。  
  
 生產資料庫稱為「*主體資料庫*」，而待命副本則稱為「*鏡像資料庫*」。 主體資料庫和鏡像資料庫必須位於個別的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體 (伺服器執行個體) 上，如有可能，也應該位於個別的電腦上。  
  
 稱為「主體伺服器」** 的實際執行伺服器執行個體會與稱為「鏡像伺服器」** 的待命伺服器執行個體進行通訊。 主體和鏡像伺服器會在資料庫鏡像*會話*中作為夥伴。 如果主體伺服器失敗，則鏡像伺服器可以透過稱為「容錯移轉」** 的處理序，使鏡像伺服器的資料庫成為主體資料庫。 例如，Partner_A 和 Partner_B 是兩個夥伴伺服器，主體資料庫一開始在 Partner_A 為主體伺服器，而鏡像資料庫位於 Partner_B 上做為鏡像伺服器。 如果 Partner_A 離線，Partner_B 上的資料庫可以故障轉而成為目前的主體資料庫。 當 Partner_A 重新加入鏡像工作階段時，它會變成鏡像伺服器而其資料庫會變成鏡像資料庫。  
  
 替代的資料庫鏡像組態提供不同層次的效能及資料安全，並支援不同形式的容錯移轉。 如需詳細資訊，請參閱[資料庫鏡像 &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-sql-server.md)。  
  
 指定鏡像資料庫名稱時，可以使用別名。  
  
> [!NOTE]  
>  如需有關初始連接嘗試和鏡像資料庫之重新連接嘗試的詳細資訊，請參閱[將用戶端連接到資料庫鏡像會話 &#40;SQL Server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)。  
  
## <a name="programming-considerations"></a>程式設計考量  
 當主體資料庫伺服器失敗時，用戶端應用程式會收到錯誤以回應 API 呼叫，這表示與資料庫的連接已經遺失。 發生這個情況時，對於資料庫的任何未認可變更都會遺失，而且目前的交易會回復。 如果發生這個情況，應用程式應該關閉連接 (或釋出資料來源物件) 然後再重新開啟它。 此連接會以透明的方式重新導向鏡像資料庫，現在當做主體伺服器使用。  
  
 建立連接時，主體伺服器會將其容錯移轉夥伴的識別傳送到容錯移轉發生時所使用的用戶端。 在應用程式嘗試在主體伺服器失敗後建立連接的情況下，用戶端不會知道容錯移轉夥伴的識別。 為了讓用戶端有機會處理此狀況，初始化屬性和相關聯的連接字串關鍵字可讓用戶端自行指定容錯移轉夥伴的識別。 只有在有可用的主體伺服器，但未使用時，才會在此狀況中使用用戶端屬性。 如果用戶端提供的容錯移轉夥伴伺服器指的不是當做容錯移轉夥伴的伺服器，伺服器就會拒絕連接。 若要讓應用程式符合組態變更，實際容錯移轉夥伴的識別可以透過檢查建立連接後的屬性來判斷。 如果第一次建立連接的嘗試失敗，您應該考慮快取處理夥伴資訊來更新連接字串或想出重試策略。  
  
> [!NOTE]  
>  如果您要在 DSN、連接字串或連接屬性 (Property)/屬性 (Attribute) 中使用此功能，您必須明確指定連接所使用的資料庫。 如果未完成此動作，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 將不會嘗試容錯移轉到夥伴資料庫。  
>   
>  鏡像是資料庫的一個功能。 使用多個資料庫的應用程式可能無法使用此功能。  
>   
>  此外，伺服器名稱不區分大小寫，但是資料庫名稱會區分大小寫。 因此，您應該確認您在 DSN 和連接字串中使用相同的大小寫。  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB 提供者  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供者透過連接和連接字串屬性支援資料庫鏡像。 SSPROP_INIT_FAILOVERPARTNER 屬性已加入到 DBPROPSET_SQLSERVERDBINIT 屬性集，而 **FailoverPartner** 關鍵字是 DBPROP_INIT_PROVIDERSTRING 的新連接字串屬性。 如需詳細資訊，請參閱搭配[使用連接字串關鍵字與 SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 只要載入提供者，就會維持容錯移轉快取，直到呼叫**CoUninitialize** ，或只要應用程式擁有 Native Client OLE DB 提供者（例如資料來源物件）所[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]管理之某些物件的參考即可。  
  
 如需[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]原生用戶端 OLE DB 提供者資料庫鏡像支援的詳細資訊，請參閱[初始化和授權屬性](../../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)。  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC 驅動程式  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] NATIVE Client ODBC 驅動程式透過連接和連接字串屬性支援資料庫鏡像。 具體而言，已加入 SQL_COPT_SS_FAILOVER_PARTNER 屬性以搭配[SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)和[SQLGetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md)函數使用;和**Failover_Partner**關鍵字已加入為新的連接字串屬性。  
  
 只要應用程式至少有配置一個環境控制代碼，就可以維持容錯移轉快取。 相反地，取消配置最後一個環境控制代碼時，容錯移轉快取就會遺失。  
  
> [!NOTE]  
>  ODBC 驅動程式管理員已經增強，可以支援容錯移轉伺服器名稱的規格。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Native Client 功能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [將用戶端連接至資料庫鏡像會話 &#40;SQL Server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)   
 [資料庫鏡像 &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
