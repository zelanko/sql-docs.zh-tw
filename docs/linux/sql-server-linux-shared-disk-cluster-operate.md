---
title: 操作容錯移轉叢集執行個體 - Linux 上的 SQL Server
description: 本文說明如何操作 Linux 上的 SQL Server 容錯移轉叢集執行個體 (FCI)。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: a29d1d61b628126d03458fced964bde7c92b6d68
ms.sourcegitcommit: 71b9ebb511c68e0c9cb32a860a443803d2cb58f5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/23/2019
ms.locfileid: "68032293"
---
# <a name="operate-failover-cluster-instance---sql-server-on-linux"></a>操作容錯移轉叢集執行個體 - Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文說明如何操作 Linux 上的 SQL Server 容錯移轉叢集執行個體 (FCI)。 如果您尚未在 Linux 上建立 SQL Server FCI，請參閱[設定容錯移轉叢集執行個體 - Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure.md)。 

## <a name="failover"></a>容錯移轉

FCI 的容錯移轉類似於 Windows Server 容錯移轉叢集 (WSFC)。 如果裝載 FCI 的叢集節點發生某種失敗情況，FCI 應該會自動容錯移轉至另一個節點。 不同於 WSFC，您無法設定慣用的擁有者，因此由 Pacemaker 挑選的節點會成為 FCI 新主機。

有時候，建議您手動將 FCI 容錯移轉至另一個節點。 此程序與 WSFC 上的 FCI 不同。 在 WSFC 上，您會以角色層級容錯移轉資源。 在 Pacemaker 中，您可以選擇要移動的資源；假設所有限制式都正確，則其他所有項目也會一併移動。 

容錯移轉的方式取決於 Linux 發行版本而定。 請遵循 Linux 發行版本的指示。

- [RHEL 或 Ubuntu](#-manual-failover-rhel-or-ubuntu)
- [SLES](#-manual-failover-sles)

## <a name = "#-manual-failover-rhel-or-ubuntu"></a> 手動容錯移轉 (RHEL 或 Ubuntu)

若要執行手動容錯移轉，請在 Red Hat Enterprise Linux (RHEL) 或 Ubuntu 伺服器上執行下列步驟。
1.  發出下列命令： 

   ```bash
   sudo pcs resource move <FCIResourceName> <NewHostNode> 
   ```

   \<FCIResourceName> 是 SQL Server FCI 的 Pacemaker 資源名稱。

   \<NewHostNode> 是您要裝載 FCI 的叢集節點名稱。 

   您將不會收到任何通知。

2.  在手動容錯移轉期間，Pacemaker 會在選擇手動移動的資源上建立位置限制式。 若要查看此限制式，請執行 `sudo pcs constraint`。

3.  在容錯移轉完成之後，請發出 `sudo pcs resource clear <FCIResourceName>` 以移除限制式。 

\<FCIResourceName> 是 FCI 的 Pacemaker 資源名稱。 

## <a name = "#-manual-failover-sles"></a> 手動容錯移轉 (SLES)


在 Suse Linux Enterprise Server (SLES) 中，使用 `migrate` 命令手動容錯移轉至 SQL Server FCI。 例如：

```bash
crm resource migrate <FCIResourceName> <NewHostNode>
```

\<FCIResourceName> 是容錯移轉叢集執行個體的資源名稱。 

\<NewHostNode> 是新目的地主機的名稱。 


<!---

|Distribution |Topic 
|----- |-----
|**Red Hat Enterprise Linux with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[Operate](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-sles-configure.md)

--->

## <a name="next-steps"></a>Next Steps

- [設定容錯移轉叢集執行個體 - Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
