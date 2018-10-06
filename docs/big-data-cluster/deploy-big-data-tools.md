---
title: 連接到 SQL Server 巨量資料叢集使用 Azure Data Studio |Microsoft Docs
description: 了解如何連線到 SQL Server 2019 的巨量資料叢集使用 Azure Data Studio。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/05/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 971fc2f8e8a77b00f3d2c5cd6390fec351ffc0f3
ms.sourcegitcommit: c7d3a903eb7f410db3a0230101d24de0af17621a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2018
ms.locfileid: "48827299"
---
# <a name="connect-to-a-sql-server-big-data-cluster-with-azure-data-studio"></a>連線到 SQL Server 的巨量資料叢集使用 Azure Data Studio

本文說明如何安裝 Azure Data Studio，SQL Server 2019 擴充功能 （預覽），然後連線至巨量資料叢集。 新的 SQL Server 2019 延伸模組包含的預覽支援[SQL Server 2019 巨量資料叢集](big-data-cluster-overview.md)，整合[notebook 體驗](notebooks-guidance.md)，和 PolyBase [Create External Table 精靈](../relational-databases/polybase/data-virtualization.md?toc=%2fsql%2fbig-data-cluster%2ftoc.json).

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="install-azure-data-studio"></a>安裝 Azure Data Studio

若要安裝 Azure Data Studio，請參閱[下載並安裝最新版的 Azure Data Studio](../azure-data-studio/download.md)。

## <a name="install-the-sql-server-2019-extension-preview"></a>安裝 SQL Server 2019 擴充功能 （預覽）

若要安裝擴充功能，請參閱[安裝 SQL Server 2019 擴充功能 （預覽）](../azure-data-studio/sql-server-2019-extension.md)。

## <a name="connect-to-the-cluster"></a>連線到叢集

當您連線至巨量資料叢集時，您可以選擇連接到 SQL Server[主要執行個體](concept-master-instance.md)或 HDFS/Spark 閘道。 下列各節示範如何連接到每個。

## <a name="master-instance"></a>主要執行個體

1. 在 Azure Data Studio，按下**F1** > **新連線**。
1. 在 **連線類型**，選取**Microsoft SQL Server**。
1. 輸入中的 SQL Server 主要執行個體的 IP 位址**伺服器名稱**(例如：  **\<IP 位址\>31433、**)。
1. 變更**資料庫名稱**要**high_value_data**資料庫。

   ![連接到主要執行個體](./media/deploy-big-data-tools/connect-to-cluster.png)

1. 按下**Connect**，而**Server 儀表板**應該會出現。

## <a name="hdfsspark-gateway"></a>HDFS/Spark 閘道

1. 在 Azure Data Studio，按下**F1** > **新連線**。
1. 在 **連線類型**，選取**巨量資料的 SQL Server 叢集**。
1. 輸入中的巨量資料叢集的 IP 位址**伺服器名稱**。

   ![連線到 HDFS/Spark 閘道](./media/deploy-big-data-tools/connect-to-cluster-hdfs-spark.png)

1. 按下**Connect**，而**Server 儀表板**應該會出現。

## <a name="next-steps"></a>後續步驟

若要執行 notebook，在 Azure Data Studio，請參閱[如何在 SQL Server 2019 預覽中使用 notebook](notebooks-guidance.md)。
