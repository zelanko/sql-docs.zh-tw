---
title: Microsoft Drivers for PHP for SQL Server 高可用性和災害復原支援 | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 73a80821-d345-4fea-b076-f4aabeb4af3e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9f67a0cc7f564683ed11ce7d7de9da5200128434
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "76929183"
---
# <a name="support-for-high-availability-disaster-recovery"></a>高可用性與災害復原的支援
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

此主題討論 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 針對高可用性和災害復原的支援 (已於 3.0 版中新增)。

從 Microsoft Drivers for PHP for SQL Server 的 3.0 版開始，您可以在連接字串中指定高可用性、災害復原可用性群組的可用性群組接聽程式，或是容錯移轉叢集執行個體作為伺服器。

**MultiSubnetFailover** 連線屬性會指出應用程式正在部署於可用性群組或容錯移轉叢集執行個體中，且驅動程式將會透過嘗試連線至所有 IP 位址來嘗試連線至主要 SQL Server 執行個體上的資料庫。 在連線到 SQL Server 可用性群組接聽程式或 SQL Server 容錯移轉叢集執行個體時，請一律指定 **MultiSubnetFailover=True**。 如果應用程式已連線到容錯移轉的 AlwaysOn 資料庫，原始連線會中斷，且應用程式必須開啟新的連線，才能在容錯移轉後繼續運作。

Always On 可用性群組的完整詳細資料，可在[高可用性、災害復原](https://docs.microsoft.com/sql/relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery) \(部分機器翻譯\) 文件頁面上找到。

## <a name="transparent-network-ip-resolution-tnir"></a>透明網路 IP 解析 (TNIR)

透明網路 IP 解析 (TNIR) 是現有 **MultiSubnetFailover** 功能的修訂版本。 其會在第一個解析的主機名稱 IP 沒有回應，且該主機名稱有多個相關聯的 IP 時，影響驅動程式的連線順序。 對應的連線選項是 **TransparentNetworkIPResolution**。 在與 **MultiSubnetFailover** 搭配的情況下，其能提供下列四個連線順序： 

- 啟用 TNIR 且停用 **MultiSubnetFailover**：嘗試一個 IP，然後以並行方式嘗試所有 IP
- 啟用 TNIR 且啟用 **MultiSubnetFailover**：以並行方式嘗試所有 IP
- 停用 TNIR 且停用 **MultiSubnetFailover**：逐一嘗試所有 IP
- 停用 TNIR 且啟用 **MultiSubnetFailover**：以並行方式嘗試所有 IP

TNIR 預設會啟用，且 **MultiSubnetFailover** 預設會停用。

此為使用 PDO_SQLSRV 驅動程式同時啟用 TNIR 和 **MultiSubnetFailover** 的範例：

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
如果連接字串中有 **MultiSubnetFailover** 和 **Failover_Partner** 連接關鍵字，則會發生連接錯誤。 如果使用 **MultiSubnetFailover**，且 SQL Server 傳回容錯移轉夥伴回應，指出其為資料庫鏡像配對的一部分，也會發生錯誤。  
  
將目前使用資料庫鏡像的 PHP 應用程式升級為多重子網路案例時，請移除 **Failover_Partner** 連線屬性，並取代成設定為 **True** 的 **MultiSubnetFailover**，然後將連接字串中的伺服器名稱取代為可用性群組接聽程式。 如果連接字串使用 **Failover_Partner** 和 **MultiSubnetFailover=true**，驅動程式會產生錯誤。 不過，如果連接字串使用 **Failover_Partner** 和 **MultiSubnetFailover=false** (或 **ApplicationIntent=ReadWrite**)，應用程式會使用資料庫鏡像。  
  
如果在可用性群組中的主要資料庫上使用資料庫鏡像，而且如果在連線到主要資料庫 (而不是可用性群組接聽程式) 的連接字串中使用 **MultiSubnetFailover=true**，驅動程式會傳回錯誤。  

[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="see-also"></a>另請參閱  
[連線到伺服器](../../connect/php/connecting-to-the-server.md)  
  
