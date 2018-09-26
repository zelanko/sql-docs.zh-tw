---
title: SQL Server Always On 可用性群組 Kubernetes 運算子全球需求
description: 這篇文章說明 SQL Server Kubernetes Always On 可用性群組運算子全球需求的參數
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2d5699ae16a02346f9dded732180b16615087d16
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/24/2018
ms.locfileid: "46715011"
---
# <a name="sql-server-always-on-availability-group-kubernetes-operator-parameters"></a>SQL Server Always On 可用性群組 Kubernetes 運算子的參數

Always On 可用性群組在 Kubernetes 上的需要操作員。 運算子說明.yaml 檔案。  中的規格的範例，請參閱[本教學課程](tutorial-sql-server-ag-kubernetes.md)。

這篇文章將說明運算子全域環境變數。

## <a name="example"></a>範例

下列範例說明的部署`mssql-operator`。

## <a name="global-environment-variables"></a>全域環境變數

* `MSSQL_K8S_POD_NAMESPACE` 
  * 必要項
  * **描述**： 運算子的 Kubernetes 命名空間。

* `MSSQL_K8S_SQL_WRITE_LEASE_PERIOD_SECONDS`
  * 選擇性
  * **描述**: sql server 外部的持續時間寫入租用來保留 sql server 的可寫入，並防止裂腦案例。 次要複本會等候此到期日之後選擇新的領導者。

* `MSSQL_K8S_MONITOR_PERIOD_SECONDS`
  * 選擇性
  * **描述**： 監視期間的可用性群組的狀態。 判斷複本新增和卸除的速度。 必須是小於`MSSQL_K8S_SQL_WRITE_LEASE_PERIOD_SECONDS`。
  * **預設**: 1

* `MSSQL_K8S_LEASE_DURATION_SECONDS`
  * 選擇性
  * **描述**： 可用性群組領導人租用的持續時間。 判斷次要複本之前重新選取 如果主要複本當機的等候時間長度。 這是不同於 SQL Server 寫入租用。 
  * **預設**: 10
  
  >[!NOTE]
  >其他設定會自動根據計算`MSSQL_K8S_LEASE_DURATION_SECONDS`。

* `MSSQL_K8S_RENEW_DEADLINE_SECONDS`
  * 選擇性
  * **描述**： 目前主要複本會重試重新整理的領導放棄前的持續時間。 必須是小於`MSSQL_K8S_LEASE_DURATION_SECONDS`。
  * **預設值**:  `MSSQL_K8S_LEASE_DURATION_SECONDS` /2

* `MSSQL_K8S_RETRY_PERIOD_SECONDS`
  * 選擇性
  * **描述**： 持續時間做[主要](http://kubernetes.io/docs/concepts/architecture/master-node-communication/)等候更新領導者租用。 必須是小於`MSSQL_K8S_LEASE_DURATION_SECONDS`。
  * **預設值**:  `MSSQL_K8S_RENEW_DEADLINE_SECONDS` /2

* `MSSQL_K8S_ACQUIRE_PERIOD_SECONDS` 
  * 選擇性
  * **描述**： 次要複本進行輪詢，如果領導者租用期已經到期的期間。 
  * **預設**: 1


  ## <a name="next-steps"></a>後續步驟

[在 Kubernetes 叢集上的 SQL Server 可用性群組](sql-server-ag-kubernetes.md)