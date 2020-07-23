---
title: 連接到設備節點
description: 本文說明各種連接到 Analytics Platform System 設備中每個節點的方式。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: b8a4936aeb696f8cca36cad419d7c64198d4b290
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942537"
---
# <a name="connect-to-appliance-nodes-in-analytics-platform-system"></a>連線至分析平臺系統中的應用裝置節點
本文說明各種連接到 Analytics Platform System 設備中每個節點的方式。  
  
## <a name="connecting-with-hadoop"></a>連接 Hadoop  
使用 Hadoop 搭配 SQL Server PDW 之前，請要求您的裝置管理員將 JAVA Runtime Environment 安裝到 SQL Server PDW 上。 如需指示，請參閱設備操作指南中的[設定與外部資料的 PolyBase 連線 &#40;分析平臺系統&#41;](configure-polybase-connectivity-to-external-data.md) 。  
  
## <a name="connecting-to-appliance-nodes"></a><a name="ConnectingToIndividualNodes"></a>連接到設備節點  
每個設備節點只會在特定使用案例和特定使用者類型的情況下，直接存取。 下表列出每個設備節點，以及使用者會直接連線到該節點的案例。  
  
<!-- MISSING LINKS For information on the purpose of each node, see [Understanding SQL Server PDW &#40;SQL Server PDW&#41;](../sqlpdw/understanding-sql-server-pdw-sql-server-pdw.md).  -->  

> [!WARNING]  
> 變更控制或計算節點上的資料庫或資料表設定，而不明確同意產品小組或 AP 的客戶支援小組可能會導致您的 AP 應用裝置不受支援。
  
|節點|存取案例|
|-|-|
|控制節點|使用網頁瀏覽器來存取管理主控台，它會在控制節點上執行。 如需詳細資訊，請參閱[使用管理主控台監視設備 &#40;分析平臺系統&#41;](monitor-the-appliance-by-using-the-admin-console.md)。<br /><br />所有用戶端應用程式和工具都會連接到控制節點，不論連接使用的是乙太網路或不受限制。<br /><br />若要設定與控制節點的乙太網路連線，請使用控制節點叢集 IP 位址和埠**17001**。 例如，"192.168.0.1，17001"。<br /><br />若要設定與控制節點的未使用連接，請使用<strong> *appliance_domain*-SQLCTL01</strong>和埠**17001**。 藉由使用<strong> *appliance_domain*SQLCTL01</strong>，應用裝置 DNS 伺服器會將您的伺服器連線到作用中的未受使用網路。 若要設定您的非應用裝置伺服器以使用此元件，請參閱設定不佔用的[網路介面卡](configure-infiniband-network-adapters.md)。<br /><br />裝置管理員會連線到控制節點來執行管理作業。 例如，裝置管理員會從控制節點執行下列作業：<br /><br />使用**dwconfig.exe**設定工具設定分析平臺系統。|  
|計算節點|計算節點連接是由控制節點所導向。 計算節點的 IP 位址永遠不會在應用程式命令中輸入為參數。<br /><br />針對載入、備份、遠端資料表複製和 Hadoop，SQL Server PDW 會直接在計算節點和非應用裝置節點或伺服器之間平行傳送或接收資料。 這些應用程式會連接到控制節點來與 SQL Server PDW 連線，然後控制節點會指示 SQL Server PDW 在計算節點與非設備伺服器之間建立通訊。<br /><br />例如，這些資料傳輸作業會與計算節點的直接連接平行發生：<br /><br />從載入伺服器載入到 SQL Server PDW。<br /><br />將資料庫從 SQL Server PDW 備份到備份伺服器。<br /><br />將資料庫從備份伺服器還原到 SQL Server PDW。<br /><br />從 SQL Server PDW 查詢 Hadoop 資料。<br /><br />將資料從 SQL Server PDW 匯出至外部 Hadoop 資料表。<br /><br />將 SQL Server PDW 資料表複製到遠端 SMP SQL Server 資料庫。|  
  
## <a name="connecting-to-the-ethernet-and-infiniband-networks"></a>連接到 Ethernet 和不會網路  
遠端伺服器可以透過設備的網路，或透過 Ethernet 網路來連接。 基於效能考慮，載入伺服器、備份伺服器和透過**CREATE REMOTE TABLE AS SELECT**語句接收資料的伺服器，通常會透過設備不會的網路傳輸資料。  
  
您可以將非設備伺服器設定為屬於您自己的客戶工作組或網域，然後使用您自己的客戶網路來連線到這些伺服器，並將資料傳送給它們。 此外，連接到設備的非應用裝置伺服器，可以選擇透過設備不會網路將資料傳輸到彼此，請小心這麼做，因為它可能會使 SQL Server PDW 的效能變慢。  
  
例如，此語句會新增網路認證，以透過「不使用」將執行備份到具有不確定 IP 位址192.168.0.1 的備份伺服器。 設備網域是*mypdw*，而語句則是從備份伺服器執行。 執行此語句之前，您必須先填入您自己的參數。  
  
```  
sqlcmd -S "mypdw-sqlctl01,17001" -U sa -P password -I -Q "exec sp_pdw_add_network_credentials '192.168.0.1', 'mypdw\Administrator', 'password'"  
```  
  
例如，載入命令會以下列程式開頭：  
  
```  
dwloader -S mypdw-SQLCTL01  
```  
  
<!-- MISSING LINKS ## See Also  
[Configure an External Windows System To Receive Remote Table Copies Using InfiniBand &#40;SQL Server PDW&#41;](../sqlpdw/configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
