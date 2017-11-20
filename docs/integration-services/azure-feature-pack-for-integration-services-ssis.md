---
title: "Azure Feature Pack for Integration Services (SSIS) |Microsoft 文件"
ms.custom: 
ms.date: 08/22/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.SSIS.AZURE.F1
- SQL14.SSIS.AZURE.F1
ms.assetid: 31de555f-ae62-4f2f-a6a6-77fea1fa8189
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 4941d8eb846e9d47b008447fe0e346d43de5d87f
ms.openlocfilehash: d4204ba56e515025bed3ae3bf8e7a77d6da471be
ms.contentlocale: zh-tw
ms.lasthandoff: 08/30/2017

---
# <a name="azure-feature-pack-for-integration-services-ssis"></a>Azure Feature Pack for Integration Services (SSIS)
SQL Server Integration Services (SSIS) Feature Pack for Azure 是提供給 SSIS 連接到 Azure 服務之間傳輸資料 Azure 和內部部署資料來源，以及處理資料儲存在 Azure 中的這個頁面列出的元件擴充功能。

[![下載 SSIS Feature Pack for Azure](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=54798) **下載**

- 適用於 SQL Server 2017- [Microsoft SQL Server 2017 Integration Services Feature Pack for Azure](https://www.microsoft.com/download/details.aspx?id=54798)
- 適用於 SQL Server 2016- [Microsoft SQL Server 2016 Integration Services Feature Pack for Azure](https://www.microsoft.com/download/details.aspx?id=49492)
- 適用於 SQL Server 2014- [Microsoft SQL Server 2014 Integration Services Feature Pack for Azure](https://www.microsoft.com/en-us/download/details.aspx?id=47366)
- 適用於 SQL Server 2012- [Microsoft SQL Server 2012 Integration Services Feature Pack for Azure](https://www.microsoft.com/en-us/download/details.aspx?id=47367)

## <a name="components-in-the-feature-pack"></a>在功能套件元件
-   連接管理員

    -   [Azure 儲存體連線管理員](../integration-services/connection-manager/azure-storage-connection-manager.md)

    -   [Azure 訂用帳戶連線管理員](../integration-services/connection-manager/azure-subscription-connection-manager.md)
    
    -   [Azure Data Lake Store 連線管理員](../integration-services/connection-manager/azure-data-lake-store-connection-manager.md)
    
    -   [Azure 資源管理員的連接管理員](../integration-services/connection-manager/azure-resource-manager-connection-manager.md)
    
    -   [Azure HDInsight 連線管理員](../integration-services/connection-manager/azure-hdinsight-connection-manager.md)

-   工作

    -   [Azure Blob 上傳工作](../integration-services/control-flow/azure-blob-upload-task.md)

    -   [Azure Blob 下載工作](../integration-services/control-flow/azure-blob-download-task.md)

    -   [Azure HDInsight Hive 工作](../integration-services/control-flow/azure-hdinsight-hive-task.md)

    -   [Azure HDInsight Pig 工作](../integration-services/control-flow/azure-hdinsight-pig-task.md)

    -   [Azure HDInsight 建立叢集工作](../integration-services/control-flow/azure-hdinsight-create-cluster-task.md)

    -   [Azure HDInsight 刪除叢集工作](../integration-services/control-flow/azure-hdinsight-delete-cluster-task.md)
    
    -   [Azure SQL DW 上傳工作](../integration-services/control-flow/azure-sql-dw-upload-task.md)

    -   [Azure Data Lake Store 檔案系統工作](../integration-services/control-flow/azure-data-lake-store-file-system-task.md)

-   資料流程元件

    -   [Azure Blob 來源](../integration-services/data-flow/azure-blob-source.md)

    -   [Azure Blob 目的地](../integration-services/data-flow/azure-blob-destination.md)
    
    -   [Azure Data Lake Store 來源](../integration-services/data-flow/azure-data-lake-store-source.md)
    
    -   [Azure Data Lake Store 目的地](../integration-services/data-flow/azure-data-lake-store-destination.md)

-   Azure Blob 和 ADLS 檔案列舉值。 請參閱[Foreach 迴圈容器](http://msdn.microsoft.com/library/95a19dde-61ca-4d9b-aa3d-131fa4264296)

## <a name="download-the-feature-pack"></a>下載功能套件
 下載 SQL Server Integration Services (SSIS) 功能套件適用於 Azure。
 
- [SSIS Azure 的功能套件](http://go.microsoft.com/fwlink/?LinkID=626967)適用於 SQL Server 2016
- [SSIS Azure 的功能套件](https://www.microsoft.com/en-us/download/details.aspx?id=54798)的[!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)]

## <a name="prerequisites"></a>필수 구성 요소
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
  

