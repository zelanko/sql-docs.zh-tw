---
title: Azure Feature Pack |Microsoft Docs
ms.custom: ''
ms.date: 08/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL11.SSIS.AZURE.F1
- SQL12.SSIS.AZURE.F1
ms.assetid: 31de555f-ae62-4f2f-a6a6-77fea1fa8189
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 536dce64880c1e70b1b8a0c4b419811c1b32a975
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62772116"
---
# <a name="azure-feature-pack"></a>Azure 功能套件
SQL Server Integration Services (SSIS) Feature Pack for Azure 是一個延伸模組，可提供此頁面上所列的元件，以便讓 SSIS 連接到 Azure 服務、在 Azure 和內部部署資料來源之間轉送資料，以及處理儲存在 Azure 中的資料。

## <a name="components-in-the-feature-pack"></a>Feature Pack 中的元件
  
-   連接管理員  
  
    -   [Azure 儲存體連線管理員](connection-manager/azure-storage-connection-manager.md)  
  
    -   [Azure 訂用帳戶連線管理員](connection-manager/azure-subscription-connection-manager.md)  
    
    -   [Azure Data Lake Store 連線管理員](../../2014/integration-services/azure-data-lake-store-connection-manager.md)
    
    -   [Azure Resource Manager 連線管理員](../../2014/integration-services/azure-resource-manager-connection-manager.md)
    
    -   [Azure HDInsight 連線管理員](../../2014/integration-services/azure-hdinsight-connection-manager.md)
  
-   工作  
  
    -   [Azure Blob 上傳工作](control-flow/azure-blob-upload-task.md)  
  
    -   [Azure Blob 下載工作](control-flow/azure-blob-download-task.md)  
  
    -   [Azure HDInsight Hive 工作](control-flow/azure-hdinsight-hive-task.md)  
  
    -   [Azure HDInsight Pig 工作](https://msdn.microsoft.com/library/mt146781(v=sql.120).aspx)
  
    -   [Azure HDInsight 建立叢集工作](control-flow/azure-hdinsight-create-cluster-task.md)  
  
    -   [Azure HDInsight 刪除叢集工作](control-flow/azure-hdinsight-delete-cluster-task.md)
    
    -   [Azure SQL DW 上傳工作](../../2014/integration-services/azure-sql-dw-upload-task.md)    
    
    -   [Azure Data Lake Store 檔案系統工作](control-flow/file-system-task.md)    
  
-   資料流程元件  
  
    -   [Azure Blob 來源](https://msdn.microsoft.com/library/mt146775(v=sql.120).aspx)  
  
    -   [Azure Blob 目的地](data-flow/azure-blob-destination.md)  
    
    -   [Azure Data Lake Store 來源](../../2014/integration-services/azure-data-lake-store-source.md)
    
    -   [Azure Data Lake Store 目的地](../../2014/integration-services/azure-data-lake-store-destination.md)
  
-   Azure Blob 列舉值與 ADLS 檔案列舉值。 請參閱 [Foreach Loop Container](control-flow/foreach-loop-container.md)。  
  
 
## <a name="download-the-feature-pack"></a>下載功能套件  
下載 SQL Server Integration Services (SSIS) Feature Pack for Azure。  
  
-   [Microsoft SQL Server 2014 Integration Services Feature Pack for Azure](https://www.microsoft.com/download/details.aspx?id=47366)  

## <a name="prerequisites"></a>先決條件  
您必須先安裝下列必要條件，再安裝這個功能套件。  
  
-   SQL Server Integration Services  
-   .Net Framework 4.5  
  
## <a name="scenarios"></a>案例  
  
### <a name="big-data-processing"></a>巨量資料處理  
 您可以使用 Azure 連接器來完成下列巨量資料處理工作：  
  
1.  使用 Azure Blob 上傳工作，將輸入資料上傳至 Azure Blob 儲存體。  
  
2.  使用 Azure HDInsight 建立叢集工作，建立 Azure HDInsight 叢集。 如果您要使用自己的叢集，這是選擇性步驟。  
  
3.  使用 Azure HDInsight 登錄區工作或 Azure HDInsight Pig 工作，在 Azure HDInsight 叢集上叫用 Pig 或登錄區工作。  
  
4.  如果在步驟 2 中建立了隨選 HDInsight 叢集，在使用過後，可使用 Azure HDInsight 刪除叢集工作來刪除該 HDInsight 叢集。  
  
5.  使用 Azure HDInsight Blob 下載工作，從 Azure Blob 儲存體下載 Pig/登錄區輸出資料。  
  
 ![SSIS-AzureConnector-BigDataScenario](media/ssis-azureconnector-bigdatascenario.png "SSIS-AzureConnector-BigDataScenario")  
  
### <a name="cloud-data-archiving"></a>雲端資料封存  
 您可以使用 SSIS 封裝中的 Azure Blob 目的地，將輸出資料寫入 Azure Blob 儲存體，或者使用 Azure Blob 來源，從 Azure Blob 儲存體讀取資料。  
  
 ![SSIS-AzureConnector-CloudArchive-1](media/ssis-azureconnector-cloudarchive-1.png "SSIS-AzureConnector-CloudArchive-1")  
  
 ![SSIS-AzureConnector-CloudArchive-2](media/ssis-azureconnector-cloudarchive-2.png "SSIS-AzureConnector-CloudArchive-2")  
  
 此外，您還可以搭配 Azure Blob 列舉程式使用 Foreach 迴圈容器，來處理多個 Bob 檔案中的資料。  
  
 ![SSIS-AzureConnector-CloudArchive-3](media/ssis-azureconnector-cloudarchive-3.png "SSIS-AzureConnector-CloudArchive-3")  
  
  
