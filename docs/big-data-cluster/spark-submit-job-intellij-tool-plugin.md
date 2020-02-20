---
title: 執行 Spark 作業：Azure Toolkit for IntelliJ
titleSuffix: SQL Server Big Data Clusters
description: 在 Azure Toolkit for IntelliJ 中於 SQL Server 巨量資料叢集上提交 Spark 作業。
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.topic: conceptual
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 70cdc7e9738abdde2dfaf479320b11a94469f661
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "75244077"
---
# <a name="submit-spark-jobs-on-big-data-clusters-2019-in-intellij"></a>在 IntelliJ 中於 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]上提交 Spark 作業

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]的其中一個主要案例是提交 Spark 作業的能力。 Spark 作業提交功能可讓您提交具有 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]參考的本機 Jar 或 Py 檔案。 也可讓您執行已位於 HDFS 檔案系統中的 Jar 或 Py 檔案。 

## <a name="prerequisites"></a>Prerequisites

- SQL Server 巨量資料叢集。
- Oracle Java 開發套件。 您可以從 [Oracle 網站](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) \(英文\) 安裝它。
- IntelliJ IDEA。 您可以從 [JetBrains 網站](https://www.jetbrains.com/idea/download/) \(英文\) 安裝它。
- Azure Toolkit for IntelliJ 擴充功能。 如需安裝指示，請參閱[安裝 Azure Toolkit for IntelliJ](https://docs.microsoft.com/azure/azure-toolkit-for-intellij-installation)。

## <a name="link-sql-server-big-data-cluster"></a>連結 SQL Server 巨量資料叢集
1. 開啟 IntelliJ IDEA 工具。

2. 如果您使用自我簽署憑證，請從 [Tools]  \(工具\) 功能表中停用 SSL 憑證驗證，選取 [Azure]  、[Validate Spark Cluster SSL Certificate]  \(驗證 Spark 叢集 SSL 憑證\)，然後 [Disable]  \(停用\)。

    ![連結 SQL Server 巨量資料叢集 - 停用 SSL](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-disableSSL.png)

3. 從 [View]  \(檢視\) 功能表開啟 Azure Explorer，選取 [Tool Windows]  \(工具視窗\)，然後選取 [Azure Explorer]  。
4. 以滑鼠右鍵按一下 [SQL Server Big Data Cluster]  \(SQL Server 巨量資料叢集\)，然後選取 [Link SQL Server Big Data Cluster]  \(連結 SQL Server 巨量資料叢集\)。 輸入 [Server]  \(伺服器\)、[User Name]  \(使用者名稱\) 和 [Password]  \(密碼\)，然後按一下 [OK]  \(確定\)。

    ![連結巨量資料叢集 - 對話方塊](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-dialog.png)

5. 當未受信任伺服器的憑證對話方塊出現時，按一下 [Accept]  \(接受\)。 您可以稍後再管理憑證，請參閱[伺服器憑證](https://www.jetbrains.com/help/idea/settings-tools-server-certificates.html) \(英文\)。

6. 已連結的叢集會列在 [SQL Server Big Data Cluster]  \(SQL Server 巨量資料叢集\) 下面。 若要監視 Spark 作業，您可以在叢集上按一下滑鼠右鍵來開啟 Spark 記錄 UI 和 Yarn UI，您也可以在此處取消連結。

    ![連結巨量資料叢集 - 操作功能表](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-contextmenu.png)

## <a name="create-a-spark-scala-application-from-spark-template"></a>從 Spark 範本建立 Spark Scala 應用程式

1. 啟動 IntelliJ IDEA，然後建立專案。 在 [New Project]  \(新增專案\) 對話方塊中，遵循下列步驟： 

   a. 選取[Azure Spark/HDInsight]   > [Spark Project with Samples (Scala)]  \(含範例的 Spark 專案 (Scala)\)。

   b. 在 [Build tool]  \(組建工具\) 清單中，根據您的需求選取下列其中一項：

      * **Maven**，適用於 Scala 專案建立精靈支援
      * **SBT**，適用於管理相依性和建置 Scala 專案

    ![[New Project] \(新增專案\) 對話方塊](./media/spark-submit-job-intellij-tool-plugin/create-hdi-scala-app.png)

2. 選取 [下一步]  。

3. Scala 專案建立精靈會自動偵測您是否已安裝 Scala 外掛程式。 選取 [安裝]  。

   ![Scala 外掛程式檢查](./media/spark-submit-job-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. 若要下載 Scala 外掛程式，請選取 [OK]  \(確定\)。 遵循指示重新啟動 IntelliJ。 

   ![Scala 外掛程式安裝對話方塊](./media/spark-submit-job-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. 在 [New Project]  \(新增專案\) 視窗中，執行下列步驟：  

    ![選取 Spark SDK](./media/spark-submit-job-intellij-tool-plugin/hdi-new-project.png)

   a. 輸入專案名稱和位置。

   b. 在 [Project SDK]  \(專案 SDK\) 下拉式清單中，針對 Spark 2.x 叢集，請選取 [Java 1.8]  ，針對 Spark 1.x 叢集，則選取 [Java 1.7]  。

   c. 在 [Spark version]  \(Spark 版本\) 下拉式清單中，Scala 專案建立精靈整合 Spark SDK 和 Scala SDK 的適當版本。 如果 Spark 叢集版本早於 2.0，請選取 [Spark 1.x]  。 否則，請選取 [Spark 2.x]  。 此範例使用 [Spark 2.0.2 (Scala 2.11.8)]  。

6. 選取 [完成]  。

7. Spark 專案會自動為您建立成品。 若要檢視該成品，請執行下列步驟：

   a. 在 [File]  \(檔案\) 功能表上，選取 [Project Structure]  \(專案結構\)。

   b. 在 [Project Structure]  \(專案結構\) 對話方塊中，選取 [Artifacts]  \(成品\) 以檢視所建立的預設成品。 您也可以選取加號 ( **+** ) 來建立自己的成品。

      ![對話方塊中的成品資訊](./media/spark-submit-job-intellij-tool-plugin/default-artifact.png)
      

## <a name="submit-application-to-sql-server-big-data-cluster"></a>將應用程式提交至 SQL Server 巨量資料叢集
連結 SQL Server 巨量資料叢集之後，您就可以將應用程式提交給它。

1. 在 [Run/Debug Configurations]  \(執行/偵錯設定\) 視窗中，按一下 [+] -> [Apache Spark on SQL Server]  \(SQL Server 上的 Apache Spark\)，選取 [Remotely Run in Cluster]  \(在叢集中遠端執行\) 索引標籤，將參數設定如下列，然後按一下 [OK] \(確定\)。

    ![互動式主控台新增設定項目](./media/spark-submit-job-intellij-tool-plugin/interactive-console-add-config-entry.png)

    ![連結巨量資料叢集 - 設定](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-config.png)

    * 針對 [Spark clusters (Linux only)]  \(Spark 叢集 (僅限 Linux)\)，選取您要在上面執行您應用程式的叢集。

    * 從 IntelliJ 專案中選取成品，或從硬碟中選取成品。

    * **Main class name** (主要類別名稱) 欄位：預設值是所選取檔案中的主要類別。 您可以選取省略號 ( **...** ) 並選擇另一個類別來變更類別。   

    * **Job Configurations** (作業設定) 欄位：預設值會設定為如上圖所示。 您可以為您的作業提交變更值或新增機碼/值。 其他資訊：[Apache Livy REST API](http://livy.incubator.apache.org./docs/latest/rest-api.html) \(英文\)

      ![Spark 提交對話方塊作業設定意義](./media/spark-submit-job-intellij-tool-plugin/submit-job-configurations.png)

    * **Command line arguments** (命令列引數) 欄位：如有需要，您可以輸入主要類別的引數值 (以空格分隔)。

    * [Referenced Jars]  \(參考的 Jar\) 和 [Referenced Files]  \(參考的檔案\) 欄位：如果有任何要參考的 Jar 或檔案，您可以輸入其路徑。 其他資訊：[Apache Spark 設定](https://spark.apache.org/docs/latest/configuration.html#runtime-environment) \(英文\) 

      ![Spark 提交對話方塊 Jar 檔案意義](./media/spark-submit-job-intellij-tool-plugin/jar-files-meaning.png)

       > [!NOTE]  
       > 若要上傳參考的 JAR 和參考的檔案，請參閱：[快速入門：使用 Azure 儲存體總管在物件儲存體中建立 Blob](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-storage-explorer)
                         
    * **Upload Path** \(上傳路徑\)：您可以指出 Jar 或 Scala 專案資源提交的儲存體位置。 有數個支援的儲存體類型：[Use Spark interactive session to upload]  \(使用 Spark 互動式工作階段上傳\) 和 [Use WebHDFS to upload]  \(使用 WebHDFS 上傳\)
    
2. 按一下 [SparkJobRun]  \(Spark 作業執行\) 來將您的專案提交至所選的叢集。 [Remote Spark Job in Cluster]  \(叢集中的遠端 Spark 作業\) 索引標籤在底部顯示作業執行進度。 您可以按一下紅色按鈕來停止應用程式。  

    ![連結巨量資料叢集 - 執行](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-run.png)

## <a name="spark-console"></a>Spark 主控台
您可以執行 Spark 本機主控台 (Scala) 或執行 Spark Livy 互動式工作階段主控台 (Scala)。

### <a name="spark-local-consolescala"></a>Spark 本機主控台 (Scala)
請確定您已滿足 WINUTILS.EXE 的先決條件。

1. 從功能表列，瀏覽至 [Run]  \(執行\) > [Edit Configurations]  \(編輯設定\)。

2. 在 [Run/Debug Configurations]  \(執行/偵錯設定\) 視窗中，於左側窗格瀏覽至 [Apache Spark on SQL Server Big Data Cluster]  \(SQL Server 巨量資料叢集上的 Apache Spark\) > [[Spark on SQL] myApp]  \([SQL 上的 Spark] myApp\)。

3. 在主視窗中，選取 [Locally Run]  \(在本機執行\) 索引標籤。

4. 提供下列值，然後選取 [OK]  \(確定\)：

    |屬性 |值 |
    |----|----|
    |作業主要類別|預設值是所選取檔案中的主要類別。 您可以選取省略號 ( **...** ) 並選擇另一個類別來變更類別。|
    |環境變數|請確定 HADOOP_HOME 的值是正確的。|
    |WINUTILS.exe 位置|請確定路徑是正確的。|

    ![本機主控台設定組態](./media/spark-submit-job-intellij-tool-plugin/console-set-configuration.png)

5. 在 [Project] \(專案\) 中，瀏覽至 [myApp]   > [src]   > [main]   > [scala]   > [myApp]  。  

6. 在功能表列中，瀏覽至 [Tools]  \(工具\) > [Spark Console]  \(Spark 主控台\) > [Run Spark Local Console(Scala)]  \(執行 Spark 本機主控台 (Scala)\)。

7. 然後可能會出現兩個對話方塊，詢問您是否要自動修正相依性。 如果需要，請選取 [Auto Fix]  \(自動修正\)。

    ![Spark 自動修正 1](./media/spark-submit-job-intellij-tool-plugin/console-auto-fix1.png)

    ![Spark 自動修正 2](./media/spark-submit-job-intellij-tool-plugin/console-auto-fix2.png)

8. 主控台看起來應該類似下面的圖片。 在主控台視窗中，輸入 `sc.appName`，然後按 Ctrl+Enter。  系統將會顯示結果。 您可以按一下紅色按鈕來終止本機主控台。

    ![本機主控台結果](./media/spark-submit-job-intellij-tool-plugin/local-console-result.png)


### <a name="spark-livy-interactive-session-consolescala"></a>Spark Livy 互動式工作階段主控台 (Scala)
只有在 IntelliJ 2018.2 和 2018.3 上才支援 Spark Livy 互動式工作階段主控台 (Scala)。

1. 從功能表列，瀏覽至 [Run]  \(執行\) > [Edit Configurations]  \(編輯設定\)。

2. 在 [Run/Debug Configurations]  \(執行/偵錯設定\) 視窗中，於左側窗格瀏覽至 [Apache Spark on SQL Server Big Data Cluster]  \(SQL Server 巨量資料叢集上的 Apache Spark\) > [[Spark on SQL] myApp]  \([SQL 上的 Spark] myApp\)。

3. 在主視窗中，選取 [Remotely Run in Cluster]  \(在叢集中遠端執行\) 索引標籤。

4. 提供下列值，然後選取 [OK]  \(確定\)：

    |屬性 |值 |
    |----|----|
    |Spark clusters (Linux only) (Spark 叢集 (僅限 Linux))|選取您要在上面執行應用程式的 SQL Server 巨量資料叢集。|
    |Main class name (主要類別名稱)|預設值是所選取檔案中的主要類別。 您可以選取省略號 ( **...** ) 並選擇另一個類別來變更類別。|

    ![互動式主控台設定組態](./media/spark-submit-job-intellij-tool-plugin/interactive-console-configuration.png)

5. 在 [Project] \(專案\) 中，瀏覽至 [myApp]   > [src]   > [main]   > [scala]   > [myApp]  。  

6. 在功能表列中，瀏覽至 [Tools]  \(工具\) > [Spark Console]  \(Spark 主控台\) > [Run Spark Livy Interactive Session Console(Scala)]  \(執行 Spark Livy 互動式工作階段主控台 (Scala)\)。

7. 主控台看起來應該類似下面的圖片。 在主控台視窗中，輸入 `sc.appName`，然後按 Ctrl+Enter。  系統將會顯示結果。 您可以按一下紅色按鈕來終止本機主控台。

    ![互動式主控台結果](./media/spark-submit-job-intellij-tool-plugin/interactive-console-result.png)

### <a name="send-selection-to-spark-console"></a>傳送所選項目至 Spark 主控台

為了方便起見，若要查看指令碼的結果，您可以將一些程式碼傳送至本機主控台或 Livy 互動式工作階段主控台 (Scala)。 您可以將 Scala 檔案中的某些程式碼反白顯示，然後以滑鼠右鍵按一下 [Send Selection To Spark Console]  \(傳送所選項目至 Spark 主控台\)。 所選的程式碼將會傳送至主控台並執行。 結果會在主控台中顯示於程式碼之後。 主控台會檢查錯誤 (如果有的話)。  

   ![傳送所選項目至 Spark 主控台](./media/spark-submit-job-intellij-tool-plugin/send-selection-to-console.png)

## <a name="next-steps"></a>後續步驟
如需有關 SQL Server 巨量資料叢集和相關案例的詳細資訊，請參閱[什麼是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]](big-data-cluster-overview.md)？
