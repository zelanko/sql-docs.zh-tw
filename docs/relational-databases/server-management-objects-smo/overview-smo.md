---
title: 概觀 (SMO) |Microsoft 文件
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: e988f9e8-6801-41d1-8069-726f487244d5
caps.latest.revision: 69
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 21d71757b4f8520e2ec2b3b7c2d1cb3c1407b420
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34708006"
---
# <a name="overview-smo"></a>概觀 (SMO)
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理物件 (SMO) 是設計來以程式設計方式管理的物件[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 您可以使用 SMO 來建立自訂的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理應用程式。 雖然 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 是一種用來管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的功能強大且廣泛的應用程式，但是可能有時候 SMO 應用程式還是會提供比較好的服務。  
  
 例如，可能必須簡化控制 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理工作的使用者應用程式，才能符合新使用者的需求及降低訓練成本。 您可能必須建立自訂的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫，或是建立一個應用程式來建立及監視索引的效率。 也可能會使用 SMO 應用程式，將協力廠商硬體或軟體緊密地併入資料庫管理應用程式中。  
  
 因為 SMO 與 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本相容，所以您可以輕鬆地管理多個版本的環境。  
  
 在 SMO 中的功能包括下列各項：  
  
-   建立快取物件模型及最佳化的物件執行個體。 只有在特別參考物件時，才會載入物件。 在建立物件時，只會載入部分的物件屬性。 剩餘的物件和屬性會在受到直接參考時載入。  
  
-   批次執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 以批次方式處理陳述式來改善網路效能。  
  
-   擷取 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 允許將任何作業擷取到指令碼中。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 會使用這個功能來為作業編碼，而不是立即執行它。  
  
-   使用 WMI 提供者管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務。 可以用程式設計的方式來啟動、停止和暫停 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務。  
  
-   進階指令碼。 可以產生 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼以重新建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件，該物件會描述與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上之其他物件的關聯性。  
  
-   使用唯一的資源名稱 (URN)。 URN 可讓您建立 SMO 物件的執行個體，並參考 SMO 物件。  
  
 SMO 也將 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 所導入的許多功能和元件表示為新的物件或屬性。 這些新元件和功能包括下列各項：  
  
-   資料表和索引資料分割，可用於資料分割配置上的資料儲存。 如需詳細資訊，請參閱 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)。  
  
-   HTTP 端點，可用於管理 SOAP 要求。 如需詳細資訊，請參閱[實作端點](../../relational-databases/server-management-objects-smo/tasks/implementing-endpoints.md)。  
  
-   快照隔離和資料列層級版本控制，可用於提升並行數。 如需詳細資訊，請參閱[使用快照隔離](../../relational-databases/native-client/features/working-with-snapshot-isolation.md)。  
  
-   XML 結構描述集合、XML 索引和 XML 資料類型會提供 XML 資料的驗證和儲存功能。 如需詳細資訊，請參閱[XML 結構描述集合&#40;SQL Server&#41; ](../../relational-databases/xml/xml-schema-collections-sql-server.md)和[使用 XML 結構描述](../../relational-databases/server-management-objects-smo/tasks/using-xml-schemas.md)。  
  
-   用於建立唯讀資料庫複本的快照集資料庫。  
  
-   [!INCLUDE[ssSB](../../includes/sssb-md.md)] 可支援以訊息為基礎的通訊。 如需詳細資訊，請參閱[SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫物件多個名稱的同義字支援。 如需詳細資訊，請參閱[同義字&#40;Database Engine&#41;](../../relational-databases/synonyms/synonyms-database-engine.md)。  
  
-   Database Mail 的管理，可讓您在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中建立電子郵件伺服器、電子郵件設定檔和電子郵件帳戶。 如需詳細資訊，請參閱 [Database Mail](../../relational-databases/database-mail/database-mail.md)。  
  
-   已註冊的伺服器支援，可用於註冊連接資訊。 如需詳細資訊，請參閱[註冊伺服器](../../tools/sql-server-management-studio/register-servers.md)。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事件的追蹤和重新執行。 如需詳細資訊，請參閱[SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)， [SQL 追蹤](../../relational-databases/sql-trace/sql-trace.md)， [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)，和[擴充事件](../../relational-databases/extended-events/extended-events.md)。  
  
-   憑證和金鑰的支援，可用於安全性控制。 如需詳細資訊，請參閱[加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)。  
  
-   DDL 觸發程序，可在 DDL 事件發生時加入功能。 如需詳細資訊，請參閱 [DDL 觸發程序](../../relational-databases/triggers/ddl-triggers.md)。  
  
 SMO 命名空間為 <xref:Microsoft.SqlServer.Management.Smo>。 SMO 會實作為[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]組件。 這表示，common language runtime 來自[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]必須安裝 2.0 版，才能使用 SMO 物件。 預設會使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SDK 選項將 SMO 組件安裝到全域組件快取 (GAC) 中。 組件位於 C:\Program Files\Microsoft SQL Server\130\SDK\Assemblies\。 如需詳細資訊，請參閱[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]文件。  
  
## <a name="smo-classes"></a>SMO 類別  
 SMO 類別包含兩種類別目錄：執行個體類別和公用程式類別。  
  
 **執行個體類別**  
  
 執行個體類別代表 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 物件，例如伺服器、資料庫、資料表、觸發程序和預存程序。 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 類別是用來建立與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的連接，並控制傳送給它之命令的擷取模式。  
  
 SMO 執行個體物件會組成一個代表資料庫伺服器階層的階層。 最上面是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體，底下是資料庫，隨後的則是資料庫、資料行、觸發程序等等。 如果一個父項對多個子項的關聯性符合邏輯 (例如具有一或多個資料行的資料表)，則子項會由物件的集合來表示。 否則子項只會由物件表示。  
  
 **公用程式類別**  
  
 公用程式類別是一組為了執行特定工作所明確建立的物件。 這些類別已經根據功能分成不同的物件階層：  
  
-   傳送類別。 這是用來將結構描述和資料傳送到另一個資料庫。  
  
-   備份和還原類別。 這些是用來備份和還原資料庫。  
  
-   Scripter 類別。 這是用來建立指令碼檔案，以便重新產生物件和它們的相依性。  
  
## <a name="smo-features"></a>SMO 功能  
 **最佳化的效能**  
  
 SMO 架構是有效率就記憶體而言，因為物件僅部分具現化一開始，並從伺服器要求最少的屬性資訊。 物件的完整具現化會延遲到明確參考該物件為止。 當要求先擷取不在屬性集內的屬性，或是當呼叫需要這類屬性的方法時，就會完整具現化物件。 對使用者而言，部分具現化和完整具現化物件之間的轉換是透明的。 此外，絕對不會擷取使用許多記憶體的某些屬性，除非有明確參考該屬性。 其中一個範例就是 <xref:Microsoft.SqlServer.Management.Smo.Database.Size%2A> 物件屬性的 <xref:Microsoft.SqlServer.Management.Smo.Database> 屬性。 但是，部分具現化確實需要更多的網路往返，而且對於應用程式而言可能不是最好的執行選項。  
  
 您可以控制具現化來配合系統環境的需要。 依賴延遲的具現化會讓應用程式所需的記憶體數量最小化，但是它可能會在參考屬性時觸發許多伺服器要求。  
  
 執行個體類別 (代表真正資料庫物件的物件) 可以存在於具現化的三個層級中。 這些是最少具現化 (一個區塊內只會讀取需求性最低的屬性)、部分具現化 (一個區塊內會讀取使用相對高量記憶體的所有屬性) 以及完整具現化。 非具現化和完整具現化是具性化的傳統狀態。 部分具現化狀態會增加效率，因為部分具現化物件不包含完整物件屬性集合的值。 部分具現化是未直接參考之物件的預設狀態。 當參考其中一個屬性時，便會產生錯誤，提示使用者進行物件的完整具現化。  
  
 **擷取執行**  
  
 直接執行是常用的執行方法。 陳述式會在發生時直接傳送給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體。 擷取執行是這項處理的替代方式。  
  
 擷取執行可讓您擷取通常應該執行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次。 這樣會讓 SMO 程式設計人員延遲指令碼、將它儲存起來供稍後執行，或是提供使用者的預覽。 例如，**建立資料庫**、**建立資料表**，和**建立索引**可以傳送一個批次中並以三個循序步驟再執行陳述式。 這項功能是由使用者利用 <xref:Microsoft.SqlServer.Management.Smo.Server.%23ctor%2A> 物件所控制。  
  
 **WMI 提供者**  
  
 WMI 提供者物件是由 SMO 所包裝。 如此可針對 SMO 程式設計人員提供一個簡單的物件模型 (該模型與 SMO 類別非常類似)，而不需要了解命名空間所表示的程式設計模型以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] WMI 提供者的詳細資料。 WMI 提供者可讓您設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務、別名及用戶端和伺服器網路程式庫。  
  
 **指令碼**  
  
 在 SMO 中，指令碼已增強並移入**Scripter**類別。 **Scripter**類別可以探索相依性、 了解物件，並可讓管理相依性階層之間的關聯性。 指令碼的主要物件是**Scripter**物件。 也有幾個支援物件可處理相依性及回應進度或錯誤事件。  
  
 **Scripter**物件支援下列進階指令碼選項：  
  
-   簡單 1 階段指令碼 (會在一個步驟中建立指令碼)  
  
-   進階 3 階段指令碼 (以三個步驟，建立指令碼相依性探索、 清單產生、 指令碼產生)  
  
-   雙向相依性探索 (允許探索相依性)  
  
-   回應進度事件  
  
-   回應錯誤事件  
  
 **唯一資源名稱**  
  
 當使用 SMO 物件程式庫時有一個重要概念，就是唯一資源名稱 (URN)。 URN 會使用與 XPath 類似的語法。 XPath 是一種階層路徑，用來指定每一層都有限定詞和函數的物件。 在 SMO 中，URN 具有兩個元素，也就是功能有限的路徑和屬性命名。 路徑是用來指定物件的位置，而屬性命名則允許某個程度的篩選。  
  
 資料庫的 URN 範例如下  
  
```  
/Server/Database[@Name='Adventureworks2012']  
```  
  
 物件的 URN 可以藉由參考它的 URN 屬性來加以擷取。 Scripter 物件也會使用 Urn 當做參數傳遞給方法的物件參考**Scripter**物件。 此外，可以針對指定的 URN **GetSmoObject**方法**伺服器**物件。 這是用來建立 SMO 物件的執行個體。  
  
## <a name="sql-server-features-represented-in-smo"></a>在 SMO 中表示的 SQL Server 功能  
 **資料表和索引資料分割**  
  
 索引資料表資料分割可讓您管理資料表中資料的散佈以及檔案群組之間的索引。 這項新功能是由 SMO 物件所表示。  
  
 **端點**  
  
 SOAP 和資料庫鏡像要求是由端點利用 <xref:Microsoft.SqlServer.Management.Smo.Endpoint> 物件所處理。  
  
 **快照集隔離/資料列層級版本控制**  
  
 快照隔離 (資料列層級版本控制) 是由新的 <xref:Microsoft.SqlServer.Management.Smo.Database> 物件屬性所表示。  
  
 **XML 結構描述命名空間、 XML 索引和 XML 資料類型**  
  
 XML 結構描述命名空間在 SMO 中是由物件集合所表示。 表示 XML 索引在 SMO 中由**索引**物件屬性。  
  
 **全文檢索搜尋的增強功能**  
  
 SMO 中提供了新的物件來表示全文檢索搜尋的增強功能。  
  
 **頁面確認**  
  
 <xref:Microsoft.SqlServer.Management.Smo.DatabaseOptions.PageVerify%2A> 物件表示資料庫頁面確認選項。  
  
 **快照集資料庫**  
  
 快照集資料庫是在某個特定時間點之指定資料庫的唯讀複本。 可以使用 <xref:Microsoft.SqlServer.Management.Smo.Database.IsDatabaseSnapshot%2A> 物件的 <xref:Microsoft.SqlServer.Management.Smo.Database> 屬性來指定快照集資料庫。  
  
 **Service Broker**  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 和它的功能是由一組物件所表示。  
  
 **索引增強功能**  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 索引增強功能是由 <xref:Microsoft.SqlServer.Management.Smo.Index> 物件中的新屬性所表示。  
  
## <a name="see-also"></a>另請參閱  
 [複寫管理物件概念](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)  
  
  
