---
title: 高可用性、恢復
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 2b06186b-4090-4728-b96b-90d6ebd9f66f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f940302db497dd02b3fc5ef89056aef29a6b64a7
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388436"
---
# <a name="sql-server-native-client-support-for-high-availability-disaster-recovery"></a>高可用性/災害復原的 SQL Server Native Client 支援
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本主題將討論適用於 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client 支援 (在 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 中所新增)。 如需 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 的詳細資訊，請參閱[可用性群組接聽程式、用戶端連接性及應用程式容錯移轉 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)、[建立及設定可用性群組 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)、[容錯移轉叢集和 AlwaysOn 可用性群組 &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md) 和[使用中次要：可讀取的次要複本 &#40;AlwaysOn 可用性群組&#41;](~/database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)。  
  
 您可以在連接字串中指定給定可用性群組的可用性群組接聽程式。 如果 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 應用程式連接到可用性群組中發生容錯移轉的資料庫，則原始連接會中斷，而且應用程式必須在容錯移轉後開啟新連接，才能繼續工作。  
  
 如果未連接到可用性群組接聽程式，而且如果多個 IP 位址與主機名稱相關聯，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 會循序逐一查看與 DNS 項目相關聯的所有 IP 位址。 如果 DNS 伺服器所傳回的第一個 IP 位址未繫結至任何網路介面卡 (NIC)，這項作業可能會很費時。 在連接到可用性群組接聽程式時，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 會嘗試平行建立與所有 IP 位址的連接，如果某個連接嘗試成功，驅動程式就會捨棄任何暫止的連接嘗試。  
  
> [!NOTE]  
>  增加連接逾時並實作連接重試邏輯可提高應用程式連接到可用性群組的機率。 此外，因為連接可能會由於可用性群組容錯移轉而失敗，所以您應該實作連接重試邏輯，並重試失敗的連接，直到重新連接為止。  
  
## <a name="connecting-with-multisubnetfailover"></a>使用 MultiSubnetFailover 進行連接  
 在連接到 SQL Server 2012 可用性群組接聽程式或 SQL Server 2012 容錯移轉叢集執行個體時，永遠指定 **MultiSubnetFailover=Yes**。 **多子網故障轉移**可在 SQL Server 2012 中更快地實現所有可用性組和故障轉移群集實例的故障轉移,並將顯著縮短單個子網和多子網始終處於拓撲上的故障轉移時間。 在多重子網路容錯移轉期間，用戶端會平行嘗試連接。 在子網路容錯移轉期間，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 會積極重試 TCP 連接。  
  
 **MultiSubnetFailover** 連接屬性指示，應用程式正在可用性群組或容錯移轉叢集執行個體中部署，而且 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 會透過嘗試連接到所有 IP 位址，嘗試連接到主要 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的資料庫。 為連接指定 **MultiSubnetFailover=Yes** 時，用戶端會重試 TCP 連接，其速度比作業系統的預設 TCP 重新傳輸間隔更快。 這樣,在故障轉移后,將快速重新連接"始終處於可用性"組或始終處於故障轉移群集實例,並且適用於單子網和多子網可用性組和故障轉移群集實例。  
  
 如需連接字串關鍵字的詳細資訊，請參閱[搭配 SQL Server Native Client 使用連接字串關鍵字](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 當連接到可用性群組接聽程式或容錯移轉叢集執行個體以外的某個項目時，指定 **MultiSubnetFailover=Yes** 將會產生負面效能影響，而且不支援這樣的處理方式。  
  
 請使用下列指導方針，連接到可用性群組或容錯移轉叢集執行個體中的伺服器：  
  
-   連接到單個子網或多子網時,請使用**多子網 Failover**連接屬性;這將提高兩者的性能。  
  
-   若要連接到可用性群組，在連接字串中指定可用性群組的可用性群組接聽程式做為伺服器。  
  
-   連接到設定超過 64 個 IP 位址的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體會導致連接失敗。  
  
-   使用**多子網Failover**連接屬性的應用程式的行為不會根據身份驗證類型(身份驗證、Kerberos 身份驗證或[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Windows身份驗證)受到影響。  
  
-   您可以增加 **loginTimeout** 的值，以容納容錯移轉時間並減少應用程式連接重試次數。  
  
-   不支援分散式工作階段。  
  
 如果唯讀路由不在作用中，在下列狀況下，連接到可用性群組中的次要複本位置將會失敗：  
  
1.  如果未設定次要複本位置接受連接。  
  
2.  如果應用程式使用**應用程式意圖_ReadWrite(** 下面討論),並且輔助副本位置配置為唯讀存取。  
  
 如果設定主要複本拒絕唯讀工作負載，而且連接字串包含 **ApplicationIntent=ReadOnly**，則連接會失敗。  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>從資料庫鏡像升級到使用多子重網路叢集  
 如果連接字串中有 **MultiSubnetFailover** 和 **Failover_Partner** 連接關鍵字，則會發生連接錯誤。 如果使用 **MultiSubnetFailover** 而且 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 傳回容錯移轉夥伴回應，指出它是資料庫鏡像配對的一部分，也會發生錯誤。  
  
 如果您將目前使用資料庫鏡像的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 應用程式升級為多重子網路案例，應該移除 **Failover_Partner** 連接屬性，以設為 **Yes** 的 **MultiSubnetFailover** 取代它，並以可用性群組接聽程式取代連接字串中的伺服器名稱。 如果連接字串使用 **Failover_Partner** 和 **MultiSubnetFailover=Yes**，驅動程式會發生錯誤。 不過，如果連接字串使用 **Failover_Partner** 和 **MultiSubnetFailover=No** (或 **ApplicationIntent=ReadWrite**)，應用程式就會使用資料庫鏡像。  
  
 如果可用性群組中的主要資料庫使用資料庫鏡像，而且如果在連接到主要資料庫 (而不是可用性群組接聽程式) 的連接字串中使用 **MultiSubnetFailover=Yes**，驅動程式會傳回錯誤。  


[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="odbc"></a>ODBC  
 已加入兩個 ODBC 連接字串關鍵字來支援 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] Native Client 中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]：  
  
-   **ApplicationIntent**  
  
-   **多子網路故障移轉**  
  
 如需 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 中 ODBC 連接字串關鍵字的詳細資訊，請參閱[搭配 SQL Server Native Client 使用連接字串關鍵字](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 同等的連接屬性如下：  
  
-   **SQL_COPT_SS_APPLICATION_INTENT**  
  
-   **SQL_COPT_SS_MULTISUBNET_FAILOVER**  
  
 如需 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 中 ODBC 連接屬性的詳細資訊，請參閱 [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)。  
  
 從 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 開始，**ApplicationIntent** 和 **MultiSubnetFailover** 關鍵字的功能將會公開在使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 驅動程式之 DSN 的 ODBC 資料來源管理員中。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 應用程式可以使用三個函數的其中一個進行連接：  
  
|函式|描述|  
|--------------|-----------------|  
|[SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)|**SQLBrowseConnect** 傳回的伺服器清單不包括 VNN。 您只會看到伺服器清單，無從得知伺服器是否為獨立伺服器或是 Windows Server 容錯移轉叢集 (WSFC) 中，包含兩個或多個已啟用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 之 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 執行個體的主要或次要伺服器。 如果您連接到伺服器而且發生失敗狀況，可能是因為您已經連接到伺服器，而且 **ApplicationIntent** 設定與伺服器組態不相容。<br /><br /> 因為 **SQLBrowseConnect** 無法辨識 Windows Server 容錯移轉叢集 (WSFC) 中，包含兩個或多個已啟用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 之 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體的伺服器，所以 **SQLBrowseConnect** 會忽略 **MultiSubnetFailover** 連接字串關鍵字。|  
|[SQLConnect](../../../relational-databases/native-client-odbc-api/sqlconnect.md)|**SQLConnect** 可透過資料來源名稱 (DSN) 或連接屬性來支援 **ApplicationIntent** 和 **MultiSubnetFailover** 。|  
|[SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md)|**SQLDriverConnect** 可透過連接字串關鍵字、連接屬性或 DSN 來支援 **ApplicationIntent** 和 **MultiSubnetFailover** 。|  
  
## <a name="ole-db"></a>OLE DB  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 中的 OLE DB 不支援 **MultiSubnetFailover** 關鍵字。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 中的 OLE DB 將會支援應用程式意圖。 OLE DB 應用程式與 ODBC 應用程式的應用程式意圖將會有相同的行為 (請參閱上面的內容)。  
  
 已加入一個 OLE DB 連接字串關鍵字來支援 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] Native Client 中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]：  
  
-   **應用程式意圖**  
  
 如需 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 中連接字串關鍵字的詳細資訊，請參閱[搭配 SQL Server Native Client 使用連接字串關鍵字](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 同等的連接屬性如下：  
  
-   **SSPROP_INIT_APPLICATIONINTENT**  
  
-   **DBPROP_INIT_PROVIDERSTRING**  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 應用程式可以使用其中一個方法來指定應用程式意圖：  
  
 **IDBInitialize::Initialize**  
 **IDBInitialize::Initialize** 會使用之前設定的屬性集合來初始化資料來源及建立資料來源物件。 將應用程式意圖指定為提供者屬性或是擴充屬性字串的一部分。  
  
 **IDataInitialize::GetDataSource**  
 **IDataInitialize::GetDataSource** 會採用可包含 **Application Intent** 關鍵字的輸入連接字串。  
  
 **IDBProperties::GetProperties**  
 **IDBProperties::GetProperties** 會擷取目前在資料來源上設定的屬性值。  您可以透過 DBPROP_INIT_PROVIDERSTRING 屬性和 SSPROP_INIT_APPLICATIONINTENT 屬性擷取 **Application Intent** 值。  
  
 **IDBProperties::SetProperties**  
 若要設定 **ApplicationIntent** 屬性值，請呼叫 **IDBProperties::SetProperties**，其傳入值為 "**ReadWrite**" 或 "**ReadOnly**" 的 **SSPROP_INIT_APPLICATIONINTENT** 屬性，或是值包含 "**ApplicationIntent=ReadOnly**" 或 "**ApplicationIntent=ReadWrite**" 的 **DBPROP_INIT_PROVIDERSTRING** 屬性。  
  
 您可以在 [資料連結屬性]**** 對話方塊中，[全部] 索引標籤的 [應用程式的意圖屬性] 欄位內指定應用程式意圖。  
  
 當建立隱含連接時，隱含連接將會使用父連接的應用程式意圖設定。 同樣地，從相同資料來源建立的多個工作階段將會繼承資料來源的應用程式意圖設定。  
  
## <a name="see-also"></a>另請參閱  
 [SQL 伺服器本機用戶端功能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [搭配 SQL Server Native Client 使用連接字串關鍵字](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
  
  
