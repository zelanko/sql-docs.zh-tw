---
title: SQL Server 巨量資料叢集 HDFS 加密區域使用指南
titleSuffix: SQL Server big data clusters
description: 本文說明如何使用 BDC 的 SQL Server HDFS 加密區域功能
author: DaniBunny
ms.author: dacoelho
ms.reviewer: mihaelab
ms.date: 10/19/2020
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 904b07913a63e226e5e45876f2fc520226411223
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92199560"
---
# <a name="sql-server-big-data-clusters-hdfs-encryption-zones-usage-guide"></a>SQL Server 巨量資料叢集 HDFS 加密區域使用指南

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

本指南示範如何使用 SQL Server 巨量資料叢集的待用加密功能，透過加密區域來加密 HDFS 資料夾。

請注意， __```/securelake```__ 上已掛接預設的加密區域可供隨時使用。 其是使用系統產生的 256 位元金鑰 (名為 __securelakekey__ ) 所建立的。 此金鑰可用來建立其他加密區域。

## <a name="prerequisites"></a><a id="prereqs"></a> 必要條件

- [具有 Active Directory 整合的 SQL Server 巨量資料叢集 CU8+](release-notes-big-data-cluster.md)。
- 具有系統管理權限的使用者。

## <a name="login-into-the-name-node"></a>登入名稱節點

使用 [Active Directory 連線指示](active-directory-connect.md)來執行叢集登入。 登入 namenode (nmnode-0-0) 以發出金鑰和加密區域命令。

   ```console
   kubectl exec -it -c hadoop -n <cluster_namespace> nmnode-0-0 -- /bin/bash
   ```

## <a name="create-an-encryption-zone-using-the-provided-system-managed-key"></a>使用提供的系統管理金鑰建立加密區域

1. 建立 HDFS 資料夾

   ```console
   hdfs dfs -mkdir -p /user/zone/folder
   ```

1. 發出加密區域建立命令，以使用 __securelakekey__ 金鑰來加密資料夾。

   ```console
   hdfs crypto -createZone -keyName securelakekey -path /user/zone/folder
   ```

## <a name="create-a-custom-new-key-and-encryption-zone"></a>建立自訂的新金鑰和加密區域

1. 使用下列模式建立 256 位元金鑰。

   ```console
   kinit hdfs
   hadoop key create mydatalakekey -size 256
   ```

1. 使用使用者金鑰來建立及加密新的 HDFS 路徑。

   ```console
   hdfs dfs -mkdir -p /user/mydatalake
   hdfs crypto -createZone -keyName mydatalakekey -path /user/mydatalake
   ```
