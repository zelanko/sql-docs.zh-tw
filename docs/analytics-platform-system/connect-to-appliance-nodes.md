---
title: 連線至設備節點 Analytics Platform System |Microsoft Docs
description: 這篇文章說明連接到每個節點，Analytics Platform System 設備中的各種方式。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: ae40d38768f081ea6c439c40059065d695ebee23
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961081"
---
# <a name="connect-to-appliance-nodes-in-analytics-platform-system"></a>連接至設備節點在 Analytics Platform System
這篇文章說明連接到每個節點，Analytics Platform System 設備中的各種方式。  
  
## <a name="connecting-with-hadoop"></a>使用 Hadoop 連接  
再搭配使用 Hadoop 與 SQL Server PDW，詢問您的應用裝置系統管理員，才能安裝 SQL Server PDW 上的 Java Runtime Environment。 如需相關指示，請參閱 <<c0> [ 設定外部資料的 PolyBase 連線&#40;Analytics Platform System&#41; ](configure-polybase-connectivity-to-external-data.md)設備 Operations guide 》 中。</c0>  
  
## <a name="ConnectingToIndividualNodes"></a>連接至設備節點  
每個應用裝置節點直接存取時只能在特定使用案例下和由特定使用者類型。 下表列出每個應用裝置節點並在其下的使用者會直接連接到該節點的案例。  
  
<!-- MISSING LINKS For information on the purpose of each node, see [Understanding SQL Server PDW &#40;SQL Server PDW&#41;](../sqlpdw/understanding-sql-server-pdw-sql-server-pdw.md).  -->  

> [!WARNING]  
> 變更資料庫或資料表的設定，而不需要明確的同意，產品小組或 AP 客戶支援小組的控制項或計算節點上可能會讓您的 APS 應用裝置，不受支援。
  
|||  
|-|-|  
|**節點**|**存取案例**|  
|控制節點|您可以使用網頁瀏覽器來存取管理主控台中，會在控制節點執行。 如需詳細資訊，請參閱 <<c0> [ 使用管理主控台來監視設備&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)。</c0><br /><br />所有的用戶端應用程式和工具連接到控制節點，不論連線是否使用乙太網路或 InfiniBand。<br /><br />若要設定乙太網路連線到控制節點，使用的控制節點的叢集 IP 位址和連接埠**接著 17001**。 例如，"192.168.0.1,17001。 」<br /><br />若要設定的控制節點的 InfiniBand 連線，請使用 <strong>*appliance_domain*-SQLCTL01</strong>與連接埠**接著 17001**。 藉由使用 <strong>*appliance_domain*-SQLCTL01</strong>，應用裝置 DNS 伺服器會將伺服器連線到作用中的 InfiniBand 網路。 若要設定您的非應用裝置伺服器使用此選項，請參閱[設定的 InfiniBand 網路介面卡](configure-infiniband-network-adapters.md)。<br /><br />應用裝置系統管理員會連接到控制節點，以執行管理作業。 比方說，應用裝置系統管理員會從 [控制] 節點，執行下列作業：<br /><br />設定與 Analytics Platform System **dwconfig.exe**組態工具。|  
|計算節點|計算節點的連接會被導向由控制節點。 做為參數，計算節點的 IP 位址永遠不會輸入到應用程式的命令。<br /><br />載入，備份中，遠端資料表複製，以及 Hadoop、 SQL Server PDW 不會傳送，或直接在計算節點和非應用裝置節點或伺服器之間的平行接收資料。 這些應用程式與 SQL Server PDW 連接連接到控制節點和控制節點然後指示來建立計算節點和非應用裝置伺服器之間通訊的 SQL Server PDW。<br /><br />比方說，這些資料傳輸作業會直接連線到計算節點的同時發生：<br /><br />從載入伺服器載入 SQL Server pdw。<br /><br />備份資料庫從 SQL Server PDW 備份伺服器。<br /><br />來自備份伺服器的資料庫還原至 SQL Server PDW 中。<br /><br />從 SQL Server PDW 查詢 Hadoop 資料。<br /><br />從 SQL Server PDW 的資料匯出至外部 Hadoop 資料表中。<br /><br />將 SQL Server PDW 資料表複製到遠端 SMP SQL Server 資料庫。|  
  
## <a name="connecting-to-the-ethernet-and-infiniband-networks"></a>連線到乙太網路和 InfiniBand 網路  
遠端伺服器可以在透過設備 InfiniBand 網路，或透過乙太網路連線。 針對效能考量，載入伺服器，備份伺服器，以及伺服器接收資料，透過**建立 REMOTE TABLE AS SELECT**陳述式，通常是資料傳送到設備的 InfiniBand 網路。  
  
您可以非應用裝置伺服器設定為屬於您自己的客戶群組或網域，並連線到這些伺服器和傳輸資料，然後使用您自己的客戶網路。 此外，非應用裝置伺服器連線到 InfiniBand 應用裝置有將設備的 InfiniBand 網路; 透過將資料傳送至每個其他選項請謹慎使用這個因為它會減緩效能的 SQL Server PDW。  
  
例如，此陳述式會將執行備份的伺服器具有 InfiniBand IP 位址 192.168.0.1 透過 InfiniBand 備份的網路認證。 設備網域*mypdw*，並從備份的伺服器執行陳述式。 之前執行此陳述式，您必須填寫您自己的參數。  
  
```  
sqlcmd -S "mypdw-sqlctl01,17001" -U sa -P password -I -Q "exec sp_pdw_add_network_credentials '192.168.0.1', 'mypdw\Administrator', 'password'"  
```  
  
例如，載入命令將會啟動具有下列：  
  
```  
dwloader -S mypdw-SQLCTL01  
```  
  
<!-- MISSING LINKS ## See Also  
[Configure an External Windows System To Receive Remote Table Copies Using InfiniBand &#40;SQL Server PDW&#41;](../sqlpdw/configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
