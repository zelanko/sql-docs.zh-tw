---
title: 高可用性、 嚴重損壞修復的 Microsoft Drivers for PHP for SQL Server 支援 |Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 73a80821-d345-4fea-b076-f4aabeb4af3e
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d75a0c4285bddc8d3c237be35a51f1904de6d60
ms.sourcegitcommit: f9d4f9c1815cff1689a68debdccff5e7ff97ccaf
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/31/2018
ms.locfileid: "39367690"
---
# <a name="support-for-high-availability-disaster-recovery"></a>高可用性與災害復原的支援
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主題討論高可用性和災害復原的 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 支援 (已新增於 3.0 版中) -- [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]。  [!INCLUDE[ssHADR](../../includes/sshadr_md.md)] 中加入 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] 支援。 如需有關 [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]的詳細資訊，請參閱《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 線上叢書》。  
  
在 3.0 版的 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 中，您可以在連線屬性中指定 (高可用性和災害復原) 可用性群組 (AG) 的可用性群組接聽程式。 如果 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 應用程式連線到容錯移轉的 AlwaysOn 資料庫，原始連線會中斷，應用程式必須開啟新的連線，才能在容錯移轉後繼續工作。  
  
如果未連線到可用性群組接聽程式，而且如果多個 IP 位址與主機名稱建立關聯，[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 會循序逐一查看與 DNS 項目建立關聯的所有 IP 位址。 如果 DNS 伺服器所傳回的第一個 IP 位址未繫結至任何網路介面卡 (NIC)，這項作業可能會很費時。 在連線到可用性群組接聽程式時，[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 會嘗試平行建立與所有 IP 位址的連線，如果某個連線嘗試成功，驅動程式就會捨棄任何暫止的連線嘗試。  
  
> [!NOTE]  
> 增加連接逾時並實作連接重試邏輯可提高應用程式連接到可用性群組的機率。 此外，因為連接可能會由於可用性群組容錯移轉而失敗，所以您應該實作連接重試邏輯，並重試失敗的連接，直到重新連接為止。  
  
## <a name="connecting-with-multisubnetfailover"></a>使用 MultiSubnetFailover 進行連接  
**MultiSubnetFailover** 連線屬性表示正在可用性群組或容錯移轉叢集執行個體中部署應用程式，而且 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 會嘗試連線到所有 IP 位址，以嘗試連線到主要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 執行個體上的資料庫。 在為連線指定 **MultiSubnetFailover=true** 時，用戶端會以比作業系統預設 TCP 重新傳輸間隔更快的速度，重試 TCP 連線。 這種方式可在容錯移轉 AlwaysOn 可用性群組或 AlwaysOn 容錯移轉叢集執行個體之後更快重新連線，且同時適用於單一和多重子網路可用性群組和容錯移轉叢集執行個體。  
  
在連線到 SQL Server 2012 可用性群組接聽程式或 SQL Server 2012 容錯移轉叢集執行個體時，永遠指定 **MultiSubnetFailover=True**。 **MultiSubnetFailover** 可讓 SQL Server 2012 中的所有可用性群組和容錯移轉叢集執行個體更快地容錯移轉，並大幅縮短單一和多重子網路 AlwaysOn 拓撲的容錯移轉時間。 在多重子網路容錯移轉期間，用戶端會平行嘗試連接。 在子網路容錯移轉期間，[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 會積極重試 TCP 連線。  
  
如需有關中連接字串關鍵字[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]，請參閱 < [Connection Options](../../connect/php/connection-options.md)。  
  
當連線到可用性群組接聽程式或容錯移轉叢集執行個體以外的某個項目時，指定 **MultiSubnetFailover=true** 會導致降低效能，所以不支援此方式。  
  
請使用下列指導方針，連接到可用性群組中的伺服器：  
  
-   如果在連接到單一子網路或多重子網路時使用 **MultiSubnetFailover** 連接屬性，則會提高兩者的效能。  
  
-   若要連接到可用性群組，在連接字串中指定可用性群組的可用性群組接聽程式做為伺服器。  
  
-   連接到設定超過 64 個 IP 位址的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 執行個體會導致連接失敗。  
  
-   根據驗證的類型，使用 **MultiSubnetFailover** 連接屬性之應用程式的行為不會受到影響：[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 驗證、Kerberos 驗證或 Windows 驗證。  
  
-   提高 **loginTimeout** 的值來配合容錯移轉時間，並減少應用程式連線重試次數。  
  
-   不支援分散式交易。  
  
如果唯讀路由不在作用中，在下列狀況下，連接到可用性群組中的次要複本位置將會失敗：  
  
- 如果未設定次要複本位置接受連接。  
  
- 如果應用程式使用 **ApplicationIntent=ReadWrite**，而且已針對唯讀存取設定次要複本位置。  
  
如果設定主要複本拒絕唯讀工作負載，而且連接字串包含 **ApplicationIntent=ReadOnly**，則連接會失敗。  

## <a name="transparent-network-ip-resolution-tnir"></a>透明網路 IP 解析 (TNIR)

透明網路 IP 解析 (TNIR) 是現有的 MultiSubnetFailover 功能的修訂。 當第一個問題解決之後，主機名稱的 IP 沒有回應，而且有多個主機名稱相關聯的 Ip，它會影響的驅動程式的連接順序。 MultiSubnetFailover 以及它們會提供下列四個連接序列： 

- TNIR 啟用和停用 MultiSubnetFailover： 嘗試一個 IP，後面接著以平行方式的所有 Ip
- 啟用 TNIR & MultiSubnetFailover 啟用： 嘗試以平行方式進行的所有 Ip
- TNIR 已停用 & MultiSubnetFailover 已停用： 嘗試進行的所有 Ip 逐一
- TNIR 已停用和啟用 MultiSubnetFailover： 嘗試以平行方式進行的所有 Ip

依預設，會啟用的 TNIR 和 MultiSubnetFailover 預設會停用。

這是啟用 TNIR 和 MultiSubnetFailover 使用 PDO_SQLSRV 驅動程式的範例：

```
<?php
$serverName = "yourservername";
$username = "yourusername";
$password = "yourpassword";
$connectionString = "sqlsrv:Server=$serverName; TransparentNetworkIPResolution=Enabled; MultiSubnetFailover=yes";
try {
    $conn = new PDO($connectionString, $username, $password, array(PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION));
    // your code 
    // more of your code
    // when done, close the connection
    unset($conn);
} catch(PDOException $e) {
    print_r($e->errorInfo);
}
?>
```

## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>從資料庫鏡像升級到使用多子重網路叢集  
如果連接字串中有 **MultiSubnetFailover** 和 **Failover_Partner** 連接關鍵字，則會發生連接錯誤。 如果使用 **MultiSubnetFailover** 而且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 傳回容錯移轉夥伴回應，指出它是資料庫鏡像配對的一部分，也會發生錯誤。  
  
如果您將目前使用資料庫鏡像的 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 應用程式升級為多重子網路案例，則應移除 **Failover_Partner** 連線屬性，並取代成設定為 **Yes** 的 **MultiSubnetFailover**，然後將連接字串中的伺服器名稱取代為可用性群組接聽程式。 如果連接字串使用 **Failover_Partner** 和 **MultiSubnetFailover=true**，驅動程式會產生錯誤。 不過，如果連接字串使用 **Failover_Partner** 和 **MultiSubnetFailover=false** (或 **ApplicationIntent=ReadWrite**)，應用程式會使用資料庫鏡像。  
  
如果在可用性群組中的主要資料庫上使用資料庫鏡像，而且如果在連線到主要資料庫 (而不是可用性群組接聽程式) 的連接字串中使用 **MultiSubnetFailover=true**，驅動程式會傳回錯誤。  


[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="see-also"></a>另請參閱  
[連線到伺服器](../../connect/php/connecting-to-the-server.md)  
  
