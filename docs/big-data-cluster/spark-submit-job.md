---
title: 在 Azure Data Studio 中於 SQL Server 巨量資料叢集上提交 Spark 作業
titleSuffix: SQL Server big data clusters
description: 在 Azure Data Studio 中於 SQL Server 巨量資料叢集上提交 Spark 作業。
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6731a753c643512cd05dbc9d7b7de2c9a064576f
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/25/2019
ms.locfileid: "68470678"
---
# <a name="submit-spark-jobs-on-sql-server-big-data-clusters-in-azure-data-studio"></a>在 Azure Data Studio 中於 SQL Server 巨量資料叢集上提交 Spark 作業

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

巨量資料叢集的其中一個主要案例，是可讓您提交適用於 SQL Server 2019 Preview 的 Spark 作業。 Spark 作業提交功能可讓您提交參考 SQL Server 2019 巨量資料叢集的本機 Jar 或 Py 檔案。 也可讓您執行已位於 HDFS 檔案系統中的 Jar 或 Py 檔案。 

## <a name="prerequisites"></a>Prerequisites

- [SQL Server 2019 巨量資料工具](deploy-big-data-tools.md)：
   - **Azure Data Studio**
   - **SQL Server 2019 延伸模組**
   - **kubectl**

- [將 Azure Data Studio 連線至您巨量資料叢集的 HDFS/Spark 閘道](connect-to-big-data-cluster.md)。

## <a name="open-spark-job-submission-dialog"></a>開啟 Spark 作業提交對話方塊

有數種方式可開啟 Spark 作業提交對話方塊。 包括儀表板、[物件總管] 中的操作功能表以及命令選擇區等等。

- 若要開啟 Spark 作業提交對話方塊，請按一下儀表板中的 [新增 Spark 作業]  。

    ![按一下儀表板的提交功能表](./media/submit-spark-job/new-spark-job.png)

- 或以滑鼠右鍵按一下 [物件總管] 中的叢集，然後從操作功能表中選取 [提交 Spark 作業]  。

    ![以滑鼠右鍵按一下檔案的提交功能表](./media/submit-spark-job/submit-spark-job-1.png)


- 若要開啟已預先填入 Jar/Py 欄位的 Spark 作業提交對話方塊，請以滑鼠右鍵按一下 [物件總管中] 的 Jar/Py 檔案，然後從操作功能表中選取 [提交 Spark 作業]  。  

    ![以滑鼠右鍵按一下叢集的提交功能表](./media/submit-spark-job/submit-spark-job.png)

- 在命令選擇區中鍵入 **Ctrl+Shift+P** (Windows) 或 **Cmd+Shift+P** (Mac) 以使用 [提交 Spark 作業]  。

    ![Windows 中的提交功能表命令選擇區](./media/submit-spark-job/submit-spark-job-3.png)

    ![Mac 中的提交功能表命令選擇區](./media/submit-spark-job/submit-spark-job-4.png)
  
 
## <a name="submit-spark-job"></a>提交 Spark 作業 

Spark 作業提交對話方塊會顯示如下。 輸入作業名稱、JAR/Py 檔案路徑、主要類別和其他欄位。 Jar/Py 檔案來源可能來自本機或 HDFS。 如果 Spark 作業具有參考 Jar、Py 檔案或其他檔案，請按一下 [進階]  索引標籤，然後輸入對應的檔案路徑。 按一下 [提交]  以提交 Spark 作業。

![新增 Spark 作業對話方塊](./media/submit-spark-job/submit-spark-job-section.png)

![進階對話方塊](./media/submit-spark-job/submit-spark-job-section-1.png)

## <a name="monitor-spark-job-submission"></a>監視 Spark 作業提交

在提交 Spark 作業之後，Spark 作業提交和執行狀態資訊即會顯示在左側的 [工作歷程記錄] 中。 進度和記錄的詳細資料，也會顯示於下方的 [輸出]  視窗中。

- 當 Spark 作業正在進行時，[工作歷程記錄]  面板和 [輸出]  視窗會重新整理進度。

    ![監視 Spark 作業進行中](./media/submit-spark-job/monitor-spark-job-submission.png)

- 當 Spark 作業順利完成時，Spark UI 和 Yarn UI 連結會出現在 [輸出]  視窗中。 如需詳細資訊，請按一下連結。

    ![輸出中的 Spark 作業連結](./media/submit-spark-job/monitor-spark-job-submission-2.png)

## <a name="next-steps"></a>後續步驟

如需 SQL Server 巨量資料叢集和相關案例的詳細資訊，請參閱[什麼是 SQL Server 巨量資料叢集](big-data-cluster-overview.md)。