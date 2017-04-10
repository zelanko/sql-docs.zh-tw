---
title: "Azure Feature Pack for Integration Services (SSIS) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "SQL13.SSIS.AZURE.F1"
  - "SQL14.SSIS.AZURE.F1"
ms.assetid: 31de555f-ae62-4f2f-a6a6-77fea1fa8189
caps.latest.revision: 19
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 15
---
# Azure Feature Pack for Integration Services (SSIS)
  適用於 SQL Server 2016 的 SQL Server Integration Services (SSIS) Feature Pack for Azure 是一個延伸模組，可提供下列元件，以便讓 SSIS 連接到 Azure、在 Azure 和內部部署資料來源之間傳輸資料，以及處理儲存在 Azure 中的資料。

[![下載 SSIS Feature Pack for Azure](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=626967) **下載**[適用於 SQL Server 2016 的 SSIS Feature Pack for Azure](http://go.microsoft.com/fwlink/?LinkID=626967)


-   連接管理員

    -   [Azure 儲存體連線管理員](../integration-services/connection-manager/azure-storage-connection-manager.md)

    -   [Azure 訂用帳戶連線管理員](../integration-services/connection-manager/azure-subscription-connection-manager.md)
    
    -   [Azure Data Lake Store 連線管理員](../integration-services/connection-manager/azure-data-lake-store-connection-manager.md)

-   工作

    -   [Azure Blob 上傳工作](../integration-services/control-flow/azure-blob-upload-task.md)

    -   [Azure Blob 下載工作](../integration-services/control-flow/azure-blob-download-task.md)

    -   [Azure HDInsight Hive 工作](../integration-services/control-flow/azure-hdinsight-hive-task.md)

    -   [Azure HDInsight Pig 工作](../integration-services/control-flow/azure-hdinsight-pig-task.md)

    -   [Azure HDInsight 建立叢集工作](../integration-services/control-flow/azure-hdinsight-create-cluster-task.md)

    -   [Azure HDInsight 刪除叢集工作](../integration-services/control-flow/azure-hdinsight-delete-cluster-task.md)
    
    -   [Azure SQL DW 上傳工作](../integration-services/control-flow/azure-sql-dw-upload-task.md)

-   資料流程元件

    -   [Azure Blob 來源](../integration-services/data-flow/azure-blob-source.md)

    -   [Azure Blob 目的地](../integration-services/data-flow/azure-blob-destination.md)
    
    -   [Azure Data Lake Store 來源](../integration-services/data-flow/azure-data-lake-store-source.md)
    
    -   [Azure Data Lake Store 目的地](../integration-services/data-flow/azure-data-lake-store-destination.md)

-   Azure Blob 列舉程式。 請參閱 [列舉值 = Foreach Azure Blob 列舉值](../../../Topic/Foreach%20Loop%20Editor%20\(Collection%20Page\).md#ForeachAzureBlob)

## <a name="download-the-feature-pack"></a>下載功能套件
 請在 [這裡](http://go.microsoft.com/fwlink/?LinkID=626967)下載適用於 SQL Server 2016 的 SQL Server Integration Services (SSIS) Feature Pack for Azure。

## <a name="prerequisites"></a>必要條件
 您必須先安裝下列必要條件，再安裝這個功能套件。

-   SQL Server Integration Services

-   .Net Framework 4.5

## <a name="scenario-processing-big-data"></a>狀況︰處理巨量資料
 您可以使用 Azure 連接器來完成下列巨量資料處理工作：

1.  使用 Azure Blob 上傳工作，將輸入資料上傳至 Azure Blob 儲存體。

2.  使用 Azure HDInsight 建立叢集工作，建立 Azure HDInsight 叢集。 如果您要使用自己的叢集，這是選擇性步驟。

3.  使用 Azure HDInsight 登錄區工作或 Azure HDInsight Pig 工作，在 Azure HDInsight 叢集上叫用 Pig 或登錄區工作。

4.  如果在步驟 2 中建立了隨選 HDInsight 叢集，在使用過後，可使用 Azure HDInsight 刪除叢集工作來刪除該 HDInsight 叢集。

5.  使用 Azure HDInsight Blob 下載工作，從 Azure Blob 儲存體下載 Pig/登錄區輸出資料。

![SSIS-AzureConnector-BigDataScenario](../integration-services/media/ssis-azureconnector-bigdatascenario.png)
 
## <a name="scenario-managing-data-in-the-cloud"></a>狀況︰管理雲端中的資料
 您可以使用 SSIS 封裝中的 Azure Blob 目的地，將輸出資料寫入 Azure Blob 儲存體，或者使用 Azure Blob 來源，從 Azure Blob 儲存體讀取資料。

![SSIS-AzureConnector-CloudArchive-1](../integration-services/media/ssis-azureconnector-cloudarchive-1.png)
 
 ![SSIS-AzureConnector-CloudArchive-2](../integration-services/media/ssis-azureconnector-cloudarchive-2.png)

 您可以搭配 Azure Blob 列舉程式使用 Foreach 迴圈容器，來處理多個 Bob 檔案中的資料。

![SSIS-AzureConnector-CloudArchive-3](../integration-services/media/ssis-azureconnector-cloudarchive-3.png)
  