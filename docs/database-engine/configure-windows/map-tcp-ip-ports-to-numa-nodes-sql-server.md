---
title: 將 TCP/IP 連接埠對應到 NUMA 節點 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- NUMA
- memory [SQL Server], NUMA
- affinity NUMA
- ports [SQL Server], working with NUMA
- CPU [SQL Server], NUMA support
- NUMA, How to map a port to a NUMA node
- NUMA affinity
- TCP/IP [SQL Server], NUMA support
- non-uniform memory access
ms.assetid: 07727642-0266-4cbc-8c55-3c367e4458ca
caps.latest.revision: 20
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6481a8eabffc9459aa742e28400db7fe1442c701
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="map-tcp-ip-ports-to-numa-nodes-sql-server"></a>將 TCP/IP 連接埠對應到 NUMA 節點 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  此主題描述如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員，將 TCP/IP 通訊埠對應到非統一記憶體存取 (NUMA) 節點。 在啟動時， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會將節點資訊寫入錯誤記錄檔。  
  
 若要判斷您想要使用之節點的節點號碼，請從錯誤記錄檔或從 **sys.dm_os_schedulers** 檢視中讀取節點資訊。 若要將 TCP/IP 位址和通訊埠設為單一或多重節點，請在通訊埠編號後面用方括號附加節點識別點陣圖 (相似性遮罩)。 可以用十進位或十六進位格式指定節點。 若要建立點陣圖，請由零開始，將節點從右到左編號，例如 76543210。 建立節點清單的二進位表示法，以 1 代表您要使用的節點，以 0 代表您不要使用的節點。 例如，若要使用 NUMA 節點 0、2 和 5，請指定 00100101。  
  
|||  
|-|-|  
|NUMA 節點號碼|76543210|  
|從右算起，0、2 和 5 的遮罩|00100101|  
  
 將二進位表示法 (00100101) 轉換成十進位 `[37]`或十六進位 `[0x25]`。 若要接聽所有節點，則不要提供節點識別碼。  
  
 如果通訊埠對應到不止一個 NUMA 節點， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會以循環方式指派節點的連接，而不會嘗試去平衡節點的負載。  
  
> [!NOTE]  
>  若要讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 能夠在每個 IP 位址的多個 TCP 通訊埠上接聽，請參閱 [設定 Database Engine 接聽多個 TCP 通訊埠](../../database-engine/configure-windows/configure-the-database-engine-to-listen-on-multiple-tcp-ports.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server 組態管理員  
  
#### <a name="to-map-a-tcpip-port-to-a-numa-node"></a>若要將 TCP/IP 通訊埠對應到 NUMA 節點  
  
1.  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員中，展開 [SQL Server 網路組態]，然後按一下 [\<執行個體名稱> 的通訊協定]。  
  
2.  在詳細資料窗格中，按兩下 [TCP/IP]。  
  
3.  在 **[IP 位址]** 索引標籤上，在對應到要設定之 IP 位址的區段中，在 **[TCP 通訊埠]** 方塊中，在通訊埠編號後面以方括號加入 NUMA 節點識別碼中。 例如，對於 TCP 通訊埠 1500 和節點 0、2 和 5，請使用 **1500[37]** 或 **1500[0x25]**。  
  
## <a name="see-also"></a>另請參閱  
 [軟體 NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)  
  
  
