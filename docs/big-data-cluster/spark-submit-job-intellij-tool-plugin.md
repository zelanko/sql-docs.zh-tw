---
title: SQL Server 的巨量資料叢集上適用於 IntelliJ 執行 Spark 作業中的 Azure 工具組
titleSuffix: SQL Server big data clusters
description: 提交適用於 IntelliJ 的 Azure 工具組中的 SQL Server 巨量資料叢集上的 Spark 作業。
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e48aebbb15b9bd684b2ed3f5d4d314191a55ba42
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59932295"
---
# <a name="submit-spark-jobs-on-sql-server-big-data-clusters-in-intellij"></a>將 SQL Server 在 IntelliJ 中的巨量資料叢集上的 Spark 作業提交

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

SQL Server 的巨量資料叢集的重要案例之一是能夠提交 Spark 作業。 Spark 作業提交功能可讓您提交參考 SQL Server 的巨量資料叢集的 Jar 或 Py 本機檔案。 它也可讓您執行 Jar 或 Py 檔案，其中已經位於 HDFS 檔案系統。 

## <a name="prerequisites"></a>先決條件

- SQL Server 的巨量資料叢集。
- Oracle Java Development Kit。 您可以安裝從[Oracle 網站](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)。
- IntelliJ IDEA。 您可以安裝從[JetBrains 網站](https://www.jetbrains.com/idea/download/)。
- 適用於 IntelliJ 的延伸模組的 azure 工具組。 如需安裝指示，請參閱[安裝 Azure Toolkit for IntelliJ](https://docs.microsoft.com/azure/azure-toolkit-for-intellij-installation)。

## <a name="link-sql-server-big-data-cluster"></a>連結 SQL Server 的巨量資料叢集
1. 開啟 IntelliJ IDEA 工具。

2. 如果您使用自我簽署的憑證，停用 SSL 憑證驗證，從**工具**功能表上，選取**Azure**，**驗證 Spark 叢集 SSL 憑證**，然後**停用**。

    ![SQL Server 的巨量資料叢集連結-停用 SSL](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-disableSSL.png)

3. 開啟從 Azure Explorer**檢視**功能表上，選取**工具 Windows**，然後選取**Azure 總管**。
4. 以滑鼠右鍵按一下**巨量資料的 SQL Server 叢集**，選取**連結的 SQL Server 的巨量資料叢集**。 輸入**伺服器**，**使用者名稱**，並**密碼**，然後按一下**確定**。

    ![巨量資料叢集-連結對話方塊](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-dialog.png)

5. 不受信任的伺服器憑證 對話方塊出現時，按一下**接受**。 您可以稍後管理的憑證，請參閱[伺服器憑證](https://www.jetbrains.com/help/idea/settings-tools-server-certificates.html)。

6. 底下列出的連結的叢集**巨量資料的 SQL Server 叢集**。 您可以藉由開啟 spark 歷程記錄 UI 和 Yarn UI 來監視 spark 作業，您可能也取消連結，以滑鼠右鍵按一下叢集上。

    ![巨量資料叢集-快顯功能表連結](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-contextmenu.png)

## <a name="create-a-spark-scala-application-from-hdinsight-template"></a>從 HDInsight 範本建立 Spark Scala 應用程式

1. 啟動 IntelliJ IDEA，然後建立專案。 在 [**新的專案**] 對話方塊中，遵循下列步驟： 

   a. 選取  **Azure 的 Spark HDInsight** > **Spark 範例 (Scala) 專案**。

   b. 在 **建置工具**清單中，選取下列項目，根據您的需求：

      * **Maven**，Scala 專案建立精靈支援
      * **SBT**，用來管理相依性並建置 Scala 專案

    ![[新增專案] 對話方塊](./media/spark-submit-job-intellij-tool-plugin/create-hdi-scala-app.png)

2. 選取 **[下一步]**。

3. Scala 專案建立精靈會自動偵測您是否已安裝 Scala 外掛程式。 選取 [安裝]。

   ![Scala 外掛程式檢查](./media/spark-submit-job-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. 若要下載 Scala 外掛程式，請選取**確定**。 請依照下列指示重新啟動 IntelliJ。 

   ![Scala 外掛程式安裝對話方塊](./media/spark-submit-job-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. 在 [**新的專案**] 視窗中，執行下列步驟：  

    ![選取 Spark SDK](./media/spark-submit-job-intellij-tool-plugin/hdi-new-project.png)

   a. 輸入專案名稱和位置。

   b. 在 **專案 SDK**下拉式清單中，選取**Java 1.8**適用於 Spark 2.x 叢集或選取**Java 1.7**適用於 Spark 1.x 叢集。

   c.  在  **Spark 版本**下拉式清單中，Scala 專案建立精靈會為 Spark SDK 和 Scala SDK 整合正確的版本。 如果 Spark 叢集版本早於 2.0，請選取**Spark 1.x**。 否則，請選取**Spark2.x**。 這個範例會使用**Spark 2.0.2 (Scala 2.11.8)**。

6. 選取 [完成]。

7. Spark 專案會自動為您建立成品。 若要檢視構件，請執行下列步驟：

   a. 在 **檔案**功能表上，選取**專案結構**。

   b. 在 **專案結構**對話方塊中，選取**成品**檢視建立的預設構件。 您也可以建立自己的構件，方法是選取加號 (**+**)。

      ![在對話方塊中的構件資訊](./media/spark-submit-job-intellij-tool-plugin/default-artifact.png)
      

## <a name="submit-application-to-sql-server-big-data-cluster"></a>應用程式提交給 SQL Server 的巨量資料叢集
在連結的 SQL Server 的巨量資料叢集之後, 您可以提交給它的應用程式。

1. 設定中的組態**執行/偵錯組態**] 視窗中，按一下 [+]-> [**SQL Server 上的 Apache Spark**，選取索引標籤**從遠端在叢集中執行**，設定做為參數然後按一下 [確定]。

    ![互動式主控台新增設定項目](./media/spark-submit-job-intellij-tool-plugin/interactive-console-add-config-entry.png)

    ![巨量資料叢集-config 連結](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-config.png)

    * 針對**Spark 叢集 (僅限 Linux)**，選取您要執行您的應用程式的叢集。

    * 從 IntelliJ 專案中，選取構件，或從硬碟中選取一個。

    * **主要類別名稱**欄位：預設值是從選取的檔案的主要類別。 您可以變更類別選取省略符號 (**...**) 並選擇另一個類別。   

    * **作業組態**欄位：預設值會設定為如上所示的圖片。 您可以變更值，或加入新的索引鍵/值的作業提交作業。 如需詳細資訊：[Apache Livy REST API](http://livy.incubator.apache.org./docs/latest/rest-api.html)

      ![提交 Spark 對話方塊方塊作業組態意義](./media/spark-submit-job-intellij-tool-plugin/submit-job-configurations.png)

    * **命令列引數**欄位：您可以輸入引數的值分割的主要類別，如有需要的空間。

    * **參考 Jar**並**參考檔案**欄位：如果有的話，您可以輸入路徑參考的 Jar 和檔案。 如需詳細資訊：[Apache Spark 設定](https://spark.apache.org/docs/latest/configuration.html#runtime-environment) 

      ![這表示提交 Spark 對話方塊中 jar 檔案](./media/spark-submit-job-intellij-tool-plugin/jar-files-meaning.png)

       > [!NOTE]  
       > 若要上傳您的參考 Jar 和參考的檔案，請參閱：[如何上傳至叢集的資源](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-storage-explorer)
                         
    * **上傳路徑**:您可以指定 Jar 或 Scala 專案資源送出的儲存位置。 有數個支援的儲存體類型：**使用 Spark 互動式工作階段來上傳**和**使用 WebHDFS，若要上傳**
    
2. 按一下  **SparkJobRun**提交您的專案選取的叢集。 **叢集中的遠端 Spark 作業**索引標籤會顯示在底部的工作執行進度。 您可以按一下紅色按鈕，以停止應用程式。  

    ![連結巨量資料叢集-執行](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-run.png)

## <a name="spark-console"></a>Spark 主控台
您可以執行 Spark 本機 Console(Scala)，或執行 Spark Livy 互動式工作階段 Console(Scala)。

### <a name="spark-local-consolescala"></a>Spark 本機 Console(Scala)
請確定您符合 WINUTILS。EXE 必要條件。

1. 從功能表列中，瀏覽至**執行** > **編輯組態...**.

2. 從**執行/偵錯組態**視窗中的，在左窗格中，瀏覽至**巨量資料的 SQL Server 叢集上的 Apache Spark** > **[在 SQL 上的 Spark] myApp**。

3. 從主視窗中，選取**在本機執行** 索引標籤。

4. 提供下列值，然後按**確定**:

    |屬性 |值 |
    |----|----|
    |作業的主要類別|預設值是從選取的檔案的主要類別。 您可以變更類別選取省略符號 (**...**) 並選擇另一個類別。|
    |環境變數|請確定 HADOOP_HOME 的值正確無誤。|
    |WINUTILS.exe 位置|請確認路徑正確。|

    ![本機主控台設定組態](./media/spark-submit-job-intellij-tool-plugin/console-set-configuration.png)

5. 從專案中，瀏覽至**myApp** > **src** > **主要** > **scala**  >  **myApp**。  

6. 從功能表列中，瀏覽至**工具** > **Spark 主控台** > **執行 Spark 本機 Console(Scala)**。

7. 然後可能顯示兩個對話方塊，詢問您是否要自動修正相依性。 若是如此，選擇**自動修正**。

    ![Spark 自動 Fix1](./media/spark-submit-job-intellij-tool-plugin/console-auto-fix1.png)

    ![Spark 自動 Fix2](./media/spark-submit-job-intellij-tool-plugin/console-auto-fix2.png)

8. [] 主控台看起來應該如下列圖片所示。 在主控台視窗輸入`sc.appName`，然後按下 ctrl + enter 鍵。  將顯示結果。 您可以按一下紅色按鈕，以終止本機主控台。

    ![本機主控台結果](./media/spark-submit-job-intellij-tool-plugin/local-console-result.png)


### <a name="spark-livy-interactive-session-consolescala"></a>Spark Livy 互動式工作階段 Console(Scala)
IntelliJ 2018.2 和 2018.3 只支援 Spark Livy 互動式工作階段 Console(Scala)。

1. 從功能表列中，瀏覽至**執行** > **編輯組態...**.

2. 從**執行/偵錯組態**視窗中的，在左窗格中，瀏覽至**巨量資料的 SQL Server 叢集上的 Apache Spark** > **[在 SQL 上的 Spark] myApp**。

3. 從主視窗中，選取**從遠端在叢集中執行** 索引標籤。

4. 提供下列值，然後按**確定**:

    |屬性 |值 |
    |----|----|
    |Spark 叢集 (僅限 Linux)|選取您想要執行您的應用程式所在的 SQL Server 的巨量資料叢集。|
    |主要類別名稱|預設值是從選取的檔案的主要類別。 您可以變更類別選取省略符號 (**...**) 並選擇另一個類別。|

    ![互動式主控台設定組態](./media/spark-submit-job-intellij-tool-plugin/interactive-console-configuration.png)

5. 從專案中，瀏覽至**myApp** > **src** > **主要** > **scala**  >  **myApp**。  

6. 從功能表列中，瀏覽至**工具** > **Spark 主控台** > **執行 Spark Livy 互動式的工作階段 Console(Scala)**。

7. [] 主控台看起來應該如下列圖片所示。 在主控台視窗輸入`sc.appName`，然後按下 ctrl + enter 鍵。  將顯示結果。 您可以按一下紅色按鈕，以終止本機主控台。

    ![互動式主控台結果](./media/spark-submit-job-intellij-tool-plugin/interactive-console-result.png)

### <a name="send-selection-to-spark-console"></a>將選取範圍傳送至 Spark 主控台

為了方便起見，您可以將一些程式碼傳送至本機主控台或 Livy 互動式工作階段 Console(Scala)，以查看指令碼結果。 您可以在 Scala 檔案中，某些程式碼反白顯示，然後以滑鼠右鍵按一下**傳送到 Spark 主控台的選取項目**。 選取的程式碼會傳送至主控台，並執行。 在主控台中的程式碼之後，將會顯示結果。 如果現有，主控台就會檢查錯誤。  

   ![將選取範圍傳送至 Spark 主控台](./media/spark-submit-job-intellij-tool-plugin/send-selection-to-console.png)

## <a name="next-steps"></a>後續步驟
如需有關 SQL Server 巨量資料叢集和相關的案例的詳細資訊，請參閱 <<c0> [ 什麼是 SQL Server 2019 巨量資料叢集](big-data-cluster-overview.md)？
