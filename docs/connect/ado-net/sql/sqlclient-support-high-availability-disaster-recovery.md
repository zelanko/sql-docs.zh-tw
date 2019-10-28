---
title: SqlClient 對高可用性、災害復原的支援
description: 描述高可用性、嚴重損壞修復（AlwaysOn）可用性群組的 SqlClient 支援。
ms.date: 08/15/2019
ms.assetid: 61e0b396-09d7-4e13-9711-7dcbcbd103a0
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: c60ade4c949574b589bf1e1e660564775b394527
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451992"
---
# <a name="sqlclient-support-for-high-availability-disaster-recovery"></a>SqlClient 對高可用性、災害復原的支援

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

本主題討論適用于 SQL Server 支援高可用性、嚴重損壞修復的 Microsoft SqlClient Data Provider--AlwaysOn 可用性群組。  SQL Server 2012 新增了 AlwaysOn 可用性群組功能。 如需 AlwaysOn 可用性群組的詳細資訊，請參閱《SQL Server 線上叢書》。  
  
現在，您可以在連線屬性中指定 (高可用性、災害復原) 可用性群組 (AG) 的可用性群組接聽程式或 SQL Server 2012 容錯移轉叢集執行個體。 如果 SqlClient 應用程式連線到容錯移轉的 AlwaysOn 資料庫，原始連線會中斷，應用程式必須開啟新的連線，才能在容錯移轉後繼續工作。  
  
如果您沒有連線到可用性群組接聽程式或 SQL Server 2012 容錯移轉叢集執行個體，或是有多個 IP 位址與主機名稱相關聯，則 SqlClient 會依序逐一查看所有與 DNS 項目相關聯的 IP 位址。 如果 DNS 伺服器所傳回的第一個 IP 位址未繫結至任何網路介面卡 (NIC)，這項作業可能會很費時。 連線到可用性群組接聽程式或 SQL Server 2012 容錯移轉叢集執行個體時，SqlClient 會嘗試平行建立與所有 IP 位址的連線，若其中一個連線嘗試成功，驅動程式會捨棄所有擱置中的連線嘗試。  
  
> [!NOTE]
>  增加連接逾時並實作連接重試邏輯可提高應用程式連接到可用性群組的機率。 此外，因為連線可能會由於容錯移轉而失敗，所以您應該實作連線重試邏輯，並重試失敗的連線，直到重新連線為止。  
  
適用于 SQL Server 的 Microsoft SqlClient Data Provider 支援下列連接屬性：  
  
- `ApplicationIntent`  
  
- `MultiSubnetFailover`  
  
您可以用程式設計的方式修改這些連接字串關鍵字：  
  
- <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.ApplicationIntent%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.MultiSubnetFailover%2A>  
  
## <a name="connecting-with-multisubnetfailover"></a>使用 MultiSubnetFailover 進行連接  
在連接到 SQL Server 2012 可用性群組接聽程式或 SQL Server 2012 容錯移轉叢集執行個體時，永遠指定 `MultiSubnetFailover=True`。 `MultiSubnetFailover` 對於 SQL Server 2012 中的所有可用性群組和容錯移轉叢集執行個體可促進更快的容錯移轉，並大幅縮短單一和多重子網路 AlwaysOn 拓撲的容錯移轉時間。 在多重子網路容錯移轉期間，用戶端會平行嘗試連接。 在子網路容錯移轉期間，會積極重試 TCP 連線。  
  
`MultiSubnetFailover` 連線屬性表示會將應用程式部署至可用性群組或 SQL Server 2012 容錯移轉叢集執行個體，且 SqlClient 將透過嘗試連線至所有 IP 位址，嘗試連線至主要 SQL Server 執行個體上的資料庫。 為連線指定 `MultiSubnetFailover=True` 時，用戶端會重試 TCP 連線，其速度比作業系統的預設 TCP 重新傳輸間隔更快。 這種方式可在容錯移轉 AlwaysOn 可用性群組或 AlwaysOn 容錯移轉叢集執行個體之後更快重新連線，且同時適用於單一和多重子網路可用性群組和容錯移轉叢集執行個體。  
  
如需 SqlClient 中連接字串關鍵字的詳細資訊，請參閱 <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>。  
  
若在連線非可用性群組接聽程式或 SQL Server 2012 容錯移轉叢集執行個體時指定 `MultiSubnetFailover=True`，可能會對效能產生負面影響，因此不受支援。  
  
請使用下列指導方針，連線到可用性群組或 SQL Server 2012 容錯移轉叢集執行個體中的伺服器：  
  
- 在連接到單一子網路或多重子網路時，使用 `MultiSubnetFailover` 連接屬性；這會提高這兩種可用性群組接聽程式的效能。  
  
- 若要連接到可用性群組，在連接字串中指定可用性群組的可用性群組接聽程式做為伺服器。  
  
- 連線到設定超過 64 個 IP 位址的 SQL Server 執行個體會導致連線失敗。  
  
- 使用 `MultiSubnetFailover` 連線屬性之應用程式的行為不受驗證類型影響：SQL Server 驗證、Kerberos 驗證或 Windows 驗證。  
  
- 提高 `Connect Timeout` 的值來配合容錯移轉時間，並減少應用程式連線重試次數。  
  
- 不支援分散式交易。  
  
 如果唯讀路由不在作用中，在下列狀況下，連線到次要複本位置將會失敗：  
  
- 如果未設定次要複本位置接受連接。  
  
- 如果應用程式使用 `ApplicationIntent=ReadWrite` (下文討論)，而且已針對唯讀存取設定次要複本位置。  
  
唯讀次要複本不支援 <xref:Microsoft.Data.SqlClient.SqlDependency>。  
  
如果設定主要複本拒絕唯讀工作負載，而且連接字串包含 `ApplicationIntent=ReadOnly`，則連接會失敗。  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>從資料庫鏡像升級到使用多重子網路叢集  
如果連接字串中有 `MultiSubnetFailover` 和 `Failover Partner` 連接關鍵字，或是使用了 `MultiSubnetFailover=True` 和 TCP 以外的通訊協定，就會發生連接錯誤（<xref:System.ArgumentException>）。 如果使用 `MultiSubnetFailover` 而且 SQL Server 傳回容錯移轉夥伴回應，指出其是資料庫鏡像配對的一部分，也會發生錯誤 (<xref:Microsoft.Data.SqlClient.SqlException>)。  
  
如果您將目前使用資料庫鏡像的 SqlClient 應用程式升級為多重子網路案例，應該移除 `Failover Partner` 連線屬性，並以設為 `True` 的 `MultiSubnetFailover` 加以取代，然後以可用性群組接聽程式取代連接字串中的伺服器名稱。 如果連接字串使用 `Failover Partner` 和 `MultiSubnetFailover=True`，驅動程式會發生錯誤。 不過，如果連接字串使用 `Failover Partner` 和 `MultiSubnetFailover=False` (或 `ApplicationIntent=ReadWrite`)，應用程式就會使用資料庫鏡像。  
  
如果在 AG 的主要資料庫上使用資料庫鏡像，而且在連線至主要資料庫 (而非可用性群組接聽程式) 的連接字串中使用 `MultiSubnetFailover=True`，則驅動程式會傳回錯誤。  
  
## <a name="specifying-application-intent"></a>指定應用程式意圖  
當 `ApplicationIntent=ReadOnly` 時，用戶端在連接到啟用 AlwaysOn 的資料庫時會要求讀取工作負載。 伺服器會在連接時和在 USE 資料庫陳述式期間，只針對啟用 AlwaysOn 的資料庫強制執行此意圖。  
  
`ApplicationIntent` 關鍵字不適用於舊版唯讀資料庫。  
  
資料庫可以允許或不允許 AlwaysOn 目標資料庫上的讀取工作負載 （這是透過 `PRIMARY_ROLE` 和 `SECONDARY_ROLE`Transact SQL 語句的 `ALLOW_CONNECTIONS` 子句來完成）。  
  
`ApplicationIntent` 關鍵字用於啟用唯讀路由。  
  
## <a name="read-only-routing"></a>唯讀路由  
唯讀路由是可確保資料庫的唯讀複本之可用性的功能。 若要啟用唯讀路由：  
  
- 您必須連接到 AlwaysOn 可用性群組的可用性群組接聽程式。  
  
- `ApplicationIntent` 連接字串關鍵字必須設為 `ReadOnly`。  
  
- 可用性群組必須由資料庫管理員設定為啟用唯讀路由。  
  
使用唯讀路由的多個連接可能不會連接至相同的唯讀複本。 資料庫同步處理的變更或伺服器路由組態的變更，可能會導致用戶端連接至不同的唯讀複本。 若要確保所有唯讀要求連接至相同的唯讀複本，請勿將可用性群組接聽程式傳遞給 `Data Source` 連接字串關鍵字。 請改為指定唯讀執行個體的名稱。  
  
唯讀路由可能比連接到主要複本的時間更長，因為唯讀路由先連接到主要複本，再尋找最佳的可讀取次要複本。 因此，您應該增加登入逾時。  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server 功能和 ADO.NET](sql-server-features-adonet.md)
