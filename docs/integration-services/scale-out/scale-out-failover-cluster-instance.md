---
title: SQL Server Integration Services (SSIS) Scale Out 透過 SQL Server 容錯移轉叢集執行個體支援高可用性 | Microsoft Docs
description: 本文描述如何使用 SQL Server 容錯移轉叢集執行個體設定 SSIS Scale Out 的高可用性
ms.custom: performance
ms.date: 04/10/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
ms.openlocfilehash: 1206d81fb146c851f11ececdcc7ae38fe20eb79d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064598"
---
# <a name="scale-out-support-for-high-availability-via-sql-server-failover-cluster-instance"></a>Scale Out 透過 SQL Server 容錯移轉叢集執行個體支援高可用性

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



若要使用 SQL Server 容錯移轉叢集執行個體在 Scale Out Master 端設定高可用性，請執行下列動作：

## <a name="1-prerequisites"></a>1.Prerequisites
設定 Windows 容錯移轉叢集。 如需相關指示，請參閱[安裝適用於 Windows Server 2012 的容錯移轉叢集功能和工具](https://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx)部落格文章。 在所有叢集節點上安裝功能和工具。

## <a name="2-install-sql-server-failover-cluster"></a>2.安裝 SQL Server 容錯移轉叢集
安裝 SQL Server 容錯移轉叢集。 如需指示，請參閱 [SQL Server 容錯移轉叢集安裝](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)。 安裝期間，在 [特徵選取] 頁面上選取 [資料庫引擎服務]。 記錄 SQL Server 網路名稱供未來的設定使用。

![SQL 網路名稱](media/sql-network-name.PNG)

將次要節點新增至 SQL Server 容錯移轉叢集。

## <a name="3-install-scale-out-master-on-the-primary-node"></a>3.在主要節點上安裝 Scale Out Master
使用非叢集安裝的安裝精靈在主要節點上安裝 Integration Services 和 Scale Out Master。 

在安裝期間，將 SQL Server 網路名稱包含在 Scale Out Master 憑證的 CN 中。

> [!NOTE]
> 如果您想要分別容錯移轉 SSISDB 和 Scale Out Master 服務，請遵循 [2.在主要節點上安裝 Scale Out Master](scale-out-support-for-high-availability.md#2-install-scale-out-master-on-the-primary-node) (Scale Out Master 設定)。

## <a name="4-install-scale-out-master-on-the-secondary-node"></a>4.在次要節點上安裝 Scale Out Master
遵循 [3.在次要節點上安裝 Scale Out Master](scale-out-support-for-high-availability.md#3-install-scale-out-master-on-the-secondary-node)

## <a name="5-update-the-scale-out-master-service-configuration-file"></a>5.更新 Scale Out Master 服務設定檔
更新主要和次要節點上的 Scale Out Master 服務設定檔：\<磁碟機\>:\Program Files\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config。 將 **SqlServerName** 更新為 [SQL Server 網路名稱]//[執行個體名稱] 或預設執行個體的 [SQL Server 網路名稱]。

## <a name="6-add-scale-out-master-service-to-sql-server-role-in-windows-failover-cluster"></a>6.將 Scale Out Master 服務新增至 Windows 容錯移轉叢集的 SQL Server 角色
在容錯移轉叢集管理員中，連線至 Scale Out 的叢集。在總管中選取角色，再以滑鼠右鍵按一下 SQL Server 角色，然後選取 [新增資源] 和 [泛型服務]。 

![泛型服務](media/generic-service.PNG)

在 [新增資源精靈] 中選取 Scale Out Master 服務，並完成精靈。 

將 Scale Out Master 服務上線。

![上線](media/bring-online.PNG)

> [!NOTE]
> 如果您想要分別容錯移轉 SSISDB 和 Scale Out Master 服務，請遵循 [7.設定 Windows 容錯移轉叢集的 Scale Out Master 服務角色](scale-out-support-for-high-availability.md#7-configure-the-scale-out-master-service-role-of-the-windows-server-failover-cluster)

## <a name="7-install-scale-out-workers"></a>7.安裝 Scale Out Worker
在背景工作節點上安裝 Scale Out Worker。 在安裝期間，為主要端點指定 https://[Sql Server 網路名稱]:[主要連接埠]。 

> [!NOTE]
> 如果您想要分別容錯移轉 SSISDB 和 Scale Out Master 服務，請指定 Scale Out Master 服務的 DNS 主機名稱，而不是 SQL Server 網路名稱。

## <a name="8-install-scale-out-worker-client-certificate"></a>8.安裝 Scale Out Worker 用戶端憑證
在 SQL Server 容錯移轉叢集中的所有節點上安裝背景工作憑證。 請參閱[安裝 Scale Out Worker 用戶端憑證](walkthrough-set-up-integration-services-scale-out.md#InstallCert)。

> [!NOTE]
> Scale Out Manager 從未支援 SQL Server 容錯移轉叢集。 如果您使用 Scale Out Manager 新增 Scale Out Worker，您仍需要將背景工作憑證手動安裝到所有的主要節點。

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱下列文章：
-   [Integration Services (SSIS) Scale Out Master](integration-services-ssis-scale-out-master.md)
-   [Integration Services (SSIS) Scale Out Worker](integration-services-ssis-scale-out-worker.md)
