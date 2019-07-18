---
ms.openlocfilehash: 6cf3dd279f33ea0c157743d4b4c11248267a0a62
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68215621"
---
3. 在所有叢集節點上，開啟 Pacemaker 防火牆連接埠。 若要使用 `firewalld` 開啟這些連接埠，請執行下列命令：

   ```bash
   sudo firewall-cmd --permanent --add-service=high-availability
   sudo firewall-cmd --reload
   ```

   > 如果防火牆沒有內建的高可用性組態，開啟 Pacemaker 的下列連接埠。
   >
   > * TCP:連接埠 2224，3121 21064
   > * UDP:連接埠 5405

1. 在所有節點上安裝 Pacemaker 封裝。

   ```bash
   sudo yum install pacemaker pcs fence-agents-all resource-agents
   ```

2. 設定安裝 Pacemaker 和 Corosync 封裝時建立的預設使用者密碼。 在所有節點上使用相同的密碼。 

   ```bash
   sudo passwd hacluster
   ```

3. 若要讓節點在重新開機後重新加入叢集，請啟用並啟動 `pcsd` 服務和 Pacemaker。 在所有節點上執行下列命令。

   ```bash
   sudo systemctl enable pcsd
   sudo systemctl start pcsd
   sudo systemctl enable pacemaker
   ```

4. 建立叢集。 若要建立叢集，請執行下列命令︰

   ```bash
   sudo pcs cluster auth <node1> <node2> <node3> -u hacluster -p <password for hacluster>
   sudo pcs cluster setup --name <clusterName> <node1> <node2> <node3> 
   sudo pcs cluster start --all
   sudo pcs cluster enable --all
   ```
   
   >[!NOTE]
   >如果您先前已在相同節點上設定叢集，執行 `pcs cluster setup` 時需要使用 `--force` 選項。 這個選項相當於執行 `pcs cluster destroy`。 若要重新啟用 Pacemaker，請執行 `sudo systemctl enable pacemaker`。

5. 安裝 SQL Server 的 SQL Server 資源代理程式。 在所有節點上執行下列命令。 

   ```bash
   sudo yum install mssql-server-ha
   ```
