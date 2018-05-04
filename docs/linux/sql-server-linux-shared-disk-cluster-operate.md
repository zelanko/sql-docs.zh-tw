---
title: 操作容錯移轉叢集執行個體-SQL Server on Linux |Microsoft 文件
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: ''
ms.openlocfilehash: 4b906da09e908d97473cbbc0a22715e1cee6d795
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="operate-failover-cluster-instance---sql-server-on-linux"></a>操作容錯移轉叢集執行個體-SQL Server on Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文說明如何運作的 SQL Server 容錯移轉叢集執行個體 (FCI) 在 Linux 上。 如果您沒有在 Linux 上建立 SQL Server FCI，請參閱[設定容錯移轉叢集執行個體-SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure.md)。 

## <a name="failover"></a>容錯移轉

Fci 的容錯移轉是類似於 Windows Server 容錯移轉叢集 (WSFC)。 如果主控 FCI 的叢集節點發生失敗的部分排序，FCI 應該自動容錯移轉，另一個節點。 不同於在 WSFC 中，沒有任何方法設定慣用的擁有者，因此 Pacemaker 選擇將新主機 fci 節點。

但有些的時候您可能想要手動容錯 FCI 到另一個節點。 處理序不像使用 Fci 在 WSFC 上相同。 在 WSFC 上，您容錯移轉的角色層級的資源。 Pacemaker，在您選擇的資源，若要移動，並假設所有條件約束正確，所有其他項目會移動以及。 

容錯移轉的方式取決於 Linux 散發套件。 請依照您的 linux 散發指示。

- [RHEL 或 Ubuntu](#rhelFailover)
- [SLES](#slesFailover)

## <a name = "#rhelFailover"></a> 手動容錯移轉 （RHEL 或 Ubuntu）

若要執行的手動容錯移轉，onn Red Hat Enterprise Linux (RHEL) 或 Ubuntu 伺服器執行下列步驟。
1.  發出下列命令： 

   ```bash
   sudo pcs resource move <FCIResourceName> <NewHostNode> 
   ```

   \<FCIResourceName > 是 SQL Server FCI 的 Pacemaker 資源名稱。

   \<NewHostNode > 是您想要主控 FCI 的叢集節點的名稱。 

   您不會收到任何通知。

2.  在手動容錯移轉，Pacemaker 位置上建立條件約束已選擇手動移動的資源。 若要查看此條件約束，請執行`sudo pcs constraint`。

3.  完成容錯移轉之後，移除條件約束，藉由發出`sudo pcs resource clear <FCIResourceName>`。 

\<FCIResourceName > fci Pacemaker 資源名稱。 

## <a name = "#slesFailover"></a> 手動容錯移轉 (SLES)


在 「 Suse Linux Enterprise Server 」 (SLES) 使用`migrate`命令手動容錯移轉至 SQL Server FCI。 例如：

```bash
crm resource migrate <FCIResourceName> <NewHostNode>
```

\<FCIResourceName > 為容錯移轉叢集執行個體的資源名稱。 

\<NewHostNode > 是新的目的地主機的名稱。 


<!---
|Distribution |Topic 
|----- |-----
|**Red Hat Enterprise Linux with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[Operate](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-sles-configure.md)
--->

## <a name="next-steps"></a>後續步驟

- [設定容錯移轉叢集執行個體的 SQL Server on Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
