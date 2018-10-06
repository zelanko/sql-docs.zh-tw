---
title: SQL Server Always On 可用性群組 Kubernetes 運算子全球需求
description: 這篇文章說明 SQL Server Kubernetes Always On 可用性群組運算子全球需求的參數
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 187517c79f14ddcbf08ffa644e65558fa0a85b38
ms.sourcegitcommit: 4832ae7557a142f361fbf0a4e2d85945dbf8fff6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/03/2018
ms.locfileid: "48251996"
---
# <a name="sql-server-always-on-availability-group-kubernetes-operator-parameters"></a>SQL Server Always On 可用性群組 Kubernetes 運算子的參數

Always On 可用性群組在 Kubernetes 上的需要操作員。 資訊清單描述運算子。 資訊清單是`.yaml`檔案。 中的規格的範例，請參閱[Always On 可用性群組的 SQL Server 容器](sql-server-ag-kubernetes.md)。

這篇文章將說明運算子全域環境變數。

## <a name="example"></a>範例

下列範例說明的部署`mssql-operator`。

## <a name="global-environment-variables"></a>全域環境變數

* `MSSQL_K8S_POD_NAMESPACE` 
  * 必要項
  * **描述**: Kubernetes 命名空間的運算子。

* `MSSQL_K8S_SQL_WRITE_LEASE_PERIOD_SECONDS`
  * 選擇性
  * **描述**: sql server 的寫入-租用的持續時間。 用來保留 sql server 的可寫入，並防止裂腦案例。 次要複本會等候此選取新的領導者之後的秒數。

* `MSSQL_K8S_MONITOR_PERIOD_SECONDS`
  * 選擇性
  * **描述**： 若要監視可用性群組的狀態的期間。 判斷複本新增和卸除的速度。 必須是小於`MSSQL_K8S_SQL_WRITE_LEASE_PERIOD_SECONDS`。
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
