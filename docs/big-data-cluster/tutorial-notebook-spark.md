---
title: 執行範例筆記本 | Microsoft Docs
titleSuffix: SQL Server big data clusters
description: 本教學課程說明如何在 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 上載入和執行範例 Spark 筆記本。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4acb5c2306064da29d3537fc881dbfc3d312ad2f
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "73844236"
---
# <a name="tutorial-run-a-sample-notebook-on-a-sql-server-big-data-cluster"></a>教學課程：在 SQL Server 巨量資料叢集上執行範例筆記本

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本教學課程示範如何在 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 上，將筆記本載入 Azure Data Studio 並在其中執行。 這可讓資料科學家和資料工程師對叢集執行 Python、R 或 Scala 程式碼。

> [!TIP]
> 如果您想要的話，也可以下載並執行用於本教學課程中命令的指令碼。 如需指示，請參閱 GitHub 上的 [Spark 範例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark)。

## <a id="prereqs"></a> 必要條件

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

1. 按兩下 [伺服器]  視窗中的 HDFS/Spark 閘道連線。 然後選取 [開啟筆記本]  。

   ![開啟筆記本](media/tutorial-notebook-spark/azure-data-studio-open-notebook.png)

1. 等候 [核心]  和目標內容 ([附加至]  ) 填入。 將 [核心]  設定為 [PySpark3]  ，並將 [附加至]  設定為巨量資料叢集端點的 IP 位址。

   ![設定 [核心] 和 [附加至]](media/tutorial-notebook-spark/set-kernel-and-attach-to.png)

## <a name="run-the-notebook-cells"></a>執行筆記本資料格

您可以按下資料格左側的播放按鈕，執行每個筆記本資料格。 資料格完成執行之後，會在筆記本中顯示結果。

![執行筆記本資料格](media/tutorial-notebook-spark/run-notebook-cell.png)

連續執行範例筆記本中的每個資料格。 如需搭配 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 使用筆記本的相關資訊，請參閱下列資源：

- [如何在 SQL Server 中使用筆記本](notebooks-guidance.md)
- [如何管理 Azure Data Studio 中的 Notebook](notebooks-how-to-manage.md)

## <a name="next-steps"></a>後續步驟

深入了解筆記本：
> [!div class="nextstepaction"]
> [了解筆記本](notebooks-guidance.md)
