---
title: 連接至應用裝置節點-Analytics Platform System |Microsoft 文件
description: 這篇文章會說明連接到每個節點，Analytics Platform System 應用裝置中的各種方式。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 2d7d634023c5fc3d0a6f522b5f60933ce3b96272
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/19/2018
ms.locfileid: "31539538"
---
# <a name="connect-to-appliance-nodes-in-analytics-platform-system"></a>連線至 Analytics Platform System 中的應用裝置節點
這篇文章會說明連接到每個節點，Analytics Platform System 應用裝置中的各種方式。  
  
## <a name="connecting-with-hadoop"></a>使用 Hadoop 連接  
之前使用 SQL Server PDW Hadoop，詢問您的應用裝置系統管理員，才能安裝到 SQL Server PDW Java Runtime Environment。 如需指示，請參閱[設定外部資料的 PolyBase 連線&#40;Analytics Platform System&#41; ](configure-polybase-connectivity-to-external-data.md)應用裝置操作指南中。  
  
## <a name="ConnectingToIndividualNodes"></a>連接至應用裝置節點  
可直接存取的每個應用裝置節點只在特定使用案例下和由特定使用者類型。 下表列出每個應用裝置節點並在其下的使用者會直接連接到該節點的案例。  
  
<!-- MISSING LINKS For information on the purpose of each node, see [Understanding SQL Server PDW &#40;SQL Server PDW&#41;](../sqlpdw/understanding-sql-server-pdw-sql-server-pdw.md).  -->  
  
|||  
|-|-|  
|**節點**|**存取案例**|  
|控制節點|您可以使用網頁瀏覽器來存取管理主控台中，控制項節點執行。 如需詳細資訊，請參閱[使用管理主控台來監視設備&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)。<br /><br />所有用戶端應用程式和工具連接到不論連接是否使用乙太網路或 InfiniBand 的控制節點。<br /><br />若要設定的控制節點的乙太網路連接，請使用控制節點的叢集 IP 位址和連接埠**接著 17001**。 例如，"192.168.0.1,17001。 」<br /><br />若要設定的控制節點的 InfiniBand 連接，請使用 ***appliance_domain *-SQLCTL01**和連接埠**接著 17001**。 使用 ***appliance_domain *-SQLCTL01**，應用裝置的 DNS 伺服器會將您的伺服器連接到作用中的 InfiniBand 網路。 若要設定使用這個非應用裝置伺服器時，請參閱[設定 InfiniBand 網路介面卡](configure-infiniband-network-adapters.md)。<br /><br />應用裝置系統管理員會連接到執行管理作業的控制節點。 比方說，應用裝置系統管理員會從 [控制] 節點，執行下列作業：<br /><br />設定與 Analytics Platform System **dwconfig.exe**組態工具。|  
|計算節點|運算節點連接會被導向由控制節點。 計算節點的 IP 位址永遠不會做為參數輸入到應用程式的命令。<br /><br />載入，備份遠端資料表的副本，以及 Hadoop、 SQL Server PDW 不傳送或接收直接在平行計算節點和非應用裝置節點或伺服器之間的資料。 這些應用程式與 SQL Server PDW 連接連接至 [控制] 節點，並控制節點然後指示來建立計算節點和伺服器之間通訊非應用裝置的 SQL Server PDW。<br /><br />比方說，這些資料傳輸作業會以平行方式來計算節點的直接連線發生：<br /><br />載入伺服器中的載入至 SQL Server PDW。<br /><br />備份資料庫從 SQL Server PDW 備份伺服器。<br /><br />從備份伺服器將資料庫還原至 SQL Server PDW。<br /><br />從 SQL Server PDW 查詢 Hadoop 資料。<br /><br />將資料從 SQL Server PDW 匯出至 Hadoop 的外部資料表。<br /><br />將 SQL Server PDW 資料表複製至遠端 SMP SQL Server 資料庫。|  
  
## <a name="connecting-to-the-ethernet-and-infiniband-networks"></a>連線至乙太網路及 InfiniBand 網路  
遠端伺服器可以在透過設備 InfiniBand 網路或透過乙太網路連線。 效能考量，載入伺服器，備份伺服器，而伺服器接收資料透過**建立遠端 TABLE AS SELECT**陳述式，通常會傳送資料透過設備 InfiniBand 網路。  
  
您可以設定為屬於您自己的客戶群組或網域的非應用裝置伺服器，然後使用您自己客戶的網路連線到這些伺服器和傳輸資料。 此外，非應用裝置的伺服器連線到 InfiniBand 應用裝置可以將資料傳送到彼此，透過設備 InfiniBand 網路; 選擇請小心使用此因為它不會降低效能的 SQL Server PDW。  
  
例如，此陳述式會將執行備份的伺服器具有 InfiniBand IP 位址 192.168.0.1 InfiniBand 透過備份網路認證。 應用裝置網域是*mypdw*，並從備份的伺服器執行陳述式。 之前執行此陳述式，您必須填寫您自己的參數。  
  
```  
sqlcmd -S "mypdw-sqlctl01,17001" -U sa -P password -I -Q "exec sp_pdw_add_network_credentials '192.168.0.1', 'mypdw\Administrator', 'password'"  
```  
  
例如，載入命令將會啟動具有下列：  
  
```  
dwloader –S mypdw-SQLCTL01  
```  
  
<!-- MISSING LINKS ## See Also  
[Configure an External Windows System To Receive Remote Table Copies Using InfiniBand &#40;SQL Server PDW&#41;](../sqlpdw/configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
