---
title: 執行使用 Spark 的範例筆記本
titleSuffix: SQL Server big data clusters
description: 本教學課程說明如何在 SQL Server 2019 巨量資料叢集上載入和執行範例 Spark 筆記本。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 03/30/2020
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 32cdcca2e4052374e7f26d59a3caf35f200cd47d
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725801"
---
# <a name="run-a-sample-notebook-using-spark"></a>執行使用 Spark 的範例筆記本

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

本教學課程示範如何在 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 上，將筆記本載入 Azure Data Studio 並在其中執行。 這可讓資料科學家和資料工程師對叢集執行 Python、R 或 Scala 程式碼。

> [!TIP]
> 如果您想要的話，也可以下載並執行用於本教學課程中命令的指令碼。 如需指示，請參閱 GitHub 上的 [Spark 範例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark)。

## <a name="prerequisites"></a><a id="prereqs"></a> 必要條件

- [巨量資料工具](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 延伸模組**
- [將範例資料載入巨量資料叢集](tutorial-load-sample-data.md)

## <a name="download-the-sample-notebook-file"></a>下載範例筆記本檔案

使用下列指示，將範例筆記本檔案 **spark-sql.ipynb** 載入 Azure Data Studio。

1. 開啟 Bash 命令提示字元 (Linux) 或 Windows PowerShell。

1. 巡覽至您要下載範例筆記本檔案的目錄。

1. 執行下列 **curl** 命令，從 GitHub 下載筆記本檔案：

   ```bash
   curl 'https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/data-loading/transform-csv-files.ipynb' -o transform-csv-files.ipynb
   ```

## <a name="open-the-notebook"></a>開啟 Notebook

下列步驟說明如何在 Azure Data Studio 中開啟筆記本檔案：

1. 在 Azure Data Studio 中，連線到巨量資料叢集的主要執行個體。 如需詳細資訊，請參閱[連線到巨量資料叢集](connect-to-big-data-cluster.md)。

1. 按兩下 [伺服器] 視窗中的 HDFS/Spark 閘道連線。 然後選取 [開啟筆記本]。

   ![開啟筆記本](media/notebook-tutorial-spark/azure-data-studio-open-notebook.png)

1. 等候 [核心] 和目標內容 ([附加至]) 填入。 將 [核心] 設定為 [PySpark3]，並將 [附加至] 設定為巨量資料叢集端點的 IP 位址。

   ![設定 [核心] 和 [附加至]](media/notebook-tutorial-spark/set-kernel-and-attach-to.png)

## <a name="run-the-notebook-cells"></a>執行筆記本資料格

您可以按下資料格左側的播放按鈕，執行每個筆記本資料格。 資料格完成執行之後，會在筆記本中顯示結果。

![執行筆記本資料格](media/notebook-tutorial-spark/run-notebook-cell.png)

連續執行範例筆記本中的每個資料格。 如需搭配 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 使用筆記本的相關資訊，請參閱下列資源：

- [如何使用筆記本](../azure-data-studio/notebooks/notebooks-guidance.md)
- [如何管理 Azure Data Studio 中的 Notebook](notebooks-manage-bdc.md)

## <a name="next-steps"></a>後續步驟

深入了解筆記本：
> [!div class="nextstepaction"]
> [如何使用筆記本](../azure-data-studio/notebooks/notebooks-guidance.md)