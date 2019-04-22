---
title: 在 Azure Data Studio 中執行 Spark 作業
titleSuffix: SQL Server big data clusters
description: 提交 Azure Data Studio 中的 SQL Server 巨量資料叢集上的 Spark 作業。
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d5354927ff0c7e1c61bf358ad73312611c18f317
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2019
ms.locfileid: "58860449"
---
# <a name="submit-spark-jobs-on-sql-server-big-data-clusters-in-azure-data-studio"></a>將 SQL Server 在 Azure 資料 Studio 中的巨量資料叢集上的 Spark 作業提交

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

巨量資料叢集的重要案例之一是提交 Spark 作業的 SQL Server 2019 預覽的功能。 Spark 作業提交功能可讓您提交參考 SQL Server 2019 巨量資料叢集的 Jar 或 Py 本機檔案。 它也可讓您執行 Jar 或 Py 檔案，其中已經位於 HDFS 檔案系統。 

## <a name="prerequisites"></a>先決條件

- [SQL Server 2019 巨量資料工具](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **SQL Server 2019 延伸模組**
   - **kubectl**

- [將 Azure 資料 Studio 連線到您的巨量資料叢集的 HDFS/Spark 閘道](connect-to-big-data-cluster.md)。

## <a name="open-spark-job-submission-dialog"></a>開啟 Spark 作業提交對話方塊
有幾種方式來開啟 Spark 作業提交對話方塊。 方式包括儀表板，在 [物件總管] 中和命令集合中心，以操作功能表。

+ 按一下 **新的 Spark 作業**儀表板以開啟 Spark 作業提交對話方塊。

    ![按一下儀表板提交功能表](./media/submit-spark-job/new-spark-job.png)
 
+ 在 [物件總管] 中的叢集上按一下滑鼠右鍵，然後選取**Submit Spark Job**從內容功能表。 此時會開啟 Spark 作業提交對話方塊。  
 
    ![以滑鼠右鍵按一下叢集來提交功能表](./media/submit-spark-job/submit-spark-job.png)

+ 在 [物件總管] 中的 Jar/Py 檔案上按一下滑鼠右鍵，然後選取**Submit Spark Job**從內容功能表。 Spark 作業提交對話方塊，來預先填入的 Jar/Py 欄位將會開啟。 
 
    ![提交以滑鼠右鍵按一下檔案功能表](./media/submit-spark-job/submit-spark-job-2.png)

+ 使用命令**Submit Spark Job**從命令選擇區輸入 Ctrl + Shift + P （在 Windows) 和 Cmd + Shift + P （在 Mac)。

    ![提交 windows 中的功能表命令選擇區](./media/submit-spark-job/submit-spark-job-3.png)

    ![送出 mac 中的功能表命令選擇區](./media/submit-spark-job/submit-spark-job-4.png)
  
 
## <a name="submit-spark-job"></a>提交 Spark 作業 
Spark 作業提交對話方塊會顯示如下所示。 輸入工作名稱、 JAR/Py 檔案路徑、 主要的類別和其他欄位。 將 Jar / Py 檔案來源可能是從本機或從 HDFS。 如果的 Spark 作業已參考的 Jar，Py 檔案或其他檔案，按一下**進階**索引標籤，然後輸入對應的檔案路徑。 按一下 **送出**提交 Spark 作業。
 
![新的 spark 作業 對話方塊](./media/submit-spark-job/submit-spark-job-section.png)

![[進階] 對話方塊](./media/submit-spark-job/submit-spark-job-section-1.png)

## <a name="monitor-spark-job-submission"></a>監視 提交 Spark 作業
提交 Spark 作業之後，Spark 作業提交和執行狀態資訊會顯示在左邊工作歷程記錄中。 和的進度和記錄檔的詳細資料也會顯示在**輸出**視窗底部。
+ Spark 作業正在進行中，當**工作歷程記錄**面板並**輸出**視窗會以進度重新整理。

![監視器 spark 作業進行中](./media/submit-spark-job/monitor-spark-job-submission.png)

+ Spark 作業處於時成功完成，您可以看到 Spark UI 和 Yarn UI 中的連結**輸出**視窗。 您可以按一下連結以取得詳細的資訊。

![在輸出中的 Spark 工作連結](./media/submit-spark-job/monitor-spark-job-submission-2.png)

## <a name="next-steps"></a>後續步驟
如需有關 SQL Server 巨量資料叢集和相關的案例的詳細資訊，請參閱 <<c0> [ 什麼是 SQL Server 的巨量資料叢集](big-data-cluster-overview.md)？

