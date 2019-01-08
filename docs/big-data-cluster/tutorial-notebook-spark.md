---
title: 執行範例 notebook |Microsoft Docs
titleSuffix: SQL Server 2019 big data clusters
description: 本教學課程會示範您可以載入的方式執行的 SQL Server 2019 巨量資料叢集 （預覽） 上的 Spark notebook 範例。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: tutorial
ms.prod: sql
ms.custom: seodec18
ms.openlocfilehash: 55d37969ec3e03a635e948cdafb73eb1922a1795
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432551"
---
# <a name="tutorial-run-a-sample-notebook-on-a-sql-server-2019-big-data-cluster"></a>教學課程：SQL Server 2019 巨量資料叢集上執行 notebook 範例

本教學課程會示範如何載入及執行 Azure Data Studio 中的 notebook，在 SQL Server 2019 巨量資料叢集 （預覽） 上。 這可讓資料科學家和資料工程師對叢集執行 Python、 R 或 Scala 程式碼。

> [!TIP]
> 如果您想，您可以下載並執行命令的指令碼，在本教學課程。 如需相關指示，請參閱 < [Spark 範例](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark)GitHub 上。

## <a id="prereqs"></a> 必要條件

- [巨量資料工具](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **SQL Server 2019 延伸模組**
- [將範例資料載入您的巨量資料叢集](tutorial-load-sample-data.md)

## <a name="download-the-sample-notebook-file"></a>下載範例 notebook 檔案

載入範例筆記本檔案中使用下列指示**spark sql.ipynb**到 Azure Data Studio。

1. 開啟 bash 命令提示字元 (Linux) 或 Windows PowerShell。

1. 瀏覽至您想要用來下載範例 notebook 檔案，以的目錄。

1. 執行下列**curl**命令，以從 GitHub 下載 notebook 檔案：

   ```bash
   curl 'https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/spark-sql.ipynb' -o spark-sql.ipynb
   ```

## <a name="open-the-notebook"></a>開啟 notebook

下列步驟示範如何在 Azure 資料 Studio 中開啟筆記本檔案：

1. 在 Azure Data Studio，連接到您的巨量資料叢集的 HDFS/Spark 閘道。 如需詳細資訊，請參閱 <<c0> [ 連接到 HDFS/Spark 閘道](connect-to-big-data-cluster.md#hdfs)。

1. 在 HDFS/Spark 閘道連按兩下**伺服器**視窗。 然後選取**開啟 Notebook**。

   ![開啟 notebook](media/tutorial-notebook-spark/azure-data-studio-open-notebook.png)

1. 等候**核心**和目標內容 (**附加至**) 填入。 設定**核心**要**PySpark3**，並將**附加至**到您的巨量資料叢集端點的 IP 位址。

   ![設定核心並附加至](media/tutorial-notebook-spark/set-kernel-and-attach-to.png)

## <a name="run-the-notebook-cells"></a>執行筆記本資料格

您可以按下儲存格的左邊的 [播放] 按鈕，以執行每個 notebook 資料格。 儲存格完成執行之後，結果會顯示在 notebook 中。

![執行 notebook 資料格](media/tutorial-notebook-spark/run-notebook-cell.png)

執行連續範例 notebook 中的每個資料格。 如需 SQL Server 的巨量資料叢集搭配使用 notebook 的詳細資訊，請參閱下列資源：

- [如何在 SQL Server 2019 預覽中使用 notebook](notebooks-guidance.md)
- [如何管理 Azure Data Studio 中的 notebook](notebooks-how-to-manage.md)

## <a name="next-steps"></a>後續步驟

深入了解 notebook:
> [!div class="nextstepaction"]
> [深入了解 notebook](notebooks-guidance.md)