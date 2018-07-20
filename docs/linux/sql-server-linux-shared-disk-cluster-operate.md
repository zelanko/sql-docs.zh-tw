---
title: 操作容錯移轉叢集執行個體-在 Linux 上的 SQL Server |Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: d78162f149b96831d61ebcc0960db67887dc853c
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2018
ms.locfileid: "39087250"
---
# <a name="operate-failover-cluster-instance---sql-server-on-linux"></a>操作容錯移轉叢集執行個體-在 Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

這篇文章說明如何操作的 SQL Server 容錯移轉叢集執行個體 (FCI) 在 Linux 上。 如果您尚未在 Linux 上建立 SQL Server FCI，請參閱[設定容錯移轉叢集執行個體-在 Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure.md)。 

## <a name="failover"></a>容錯移轉

Fci 的容錯移轉是類似於 Windows Server 容錯移轉叢集 (WSFC)。 如果裝載 FCI 的叢集節點發生某種失敗，FCI 應該會自動容錯移轉，到另一個節點。 不同於 WSFC，沒有方法設定慣用的擁有者，因此 Pacemaker 選擇會是新的主機，fci 節點。

有些的時候您可能想要以手動方式容錯到另一個節點 FCI。 此程序不是與 Fci 在 WSFC 上相同。 在 WSFC 容錯移轉的角色層級的資源。 在 Pacemaker 中，選擇要移動的資源且假設所有條件約束正確，所有其他項目會將以及。 

容錯移轉的方式需視 Linux 散發套件而定。 遵循您 linux 散發套件的指示。

- [RHEL 或 Ubuntu](#rhelFailover)
- [SLES](#slesFailover)

## <a name = "#rhelFailover"></a> 手動容錯移轉 （RHEL 或 Ubuntu）

若要執行的手動容錯移轉，Red Hat Enterprise Linux (RHEL) 上或 Ubuntu 伺服器執行下列步驟。
1.  發出下列命令： 

   ```bash
   sudo pcs resource move <FCIResourceName> <NewHostNode> 
   ```

   \<FCIResourceName > 是 SQL Server fci 的 Pacemaker 資源名稱。

   \<NewHostNode > 是您想要裝載 FCI 的叢集節點的名稱。 

   您不會收到任何通知。

2.  手動容錯移轉期間，Pacemaker 會建立已選擇手動移動資源的位置條件約束。 若要查看此條件約束，請執行`sudo pcs constraint`。

3.  完成容錯移轉之後，移除條件約束，藉由發出`sudo pcs resource clear <FCIResourceName>`。 

\<FCIResourceName > 是 fci 的 Pacemaker 資源名稱。 

## <a name = "#slesFailover"></a> 手動容錯移轉 (SLES)


在 Suse Linux Enterprise Server (SLES)，使用`migrate`命令來手動容錯移轉 SQL Server FCI。 例如：

```bash
crm resource migrate <FCIResourceName> <NewHostNode>
```

\<FCIResourceName > 容錯移轉叢集執行個體的資源名稱。 

\<NewHostNode > 新的目的地主機的名稱。 


<!---
|Distribution |Topic 
|----- |-----
|**Red Hat Enterprise Linux with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[Operate](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-sles-configure.md)
--->

## <a name="next-steps"></a>後續步驟

- [設定容錯移轉叢集執行個體-在 Linux 上的 SQL Server](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
