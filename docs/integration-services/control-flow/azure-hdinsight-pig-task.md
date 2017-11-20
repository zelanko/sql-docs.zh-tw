---
title: "Azure HDInsight Pig 工作 |Microsoft 文件"
ms.custom: 
ms.date: 02/28/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.afppigtask.f1
- sql14.dts.designer.afppigtask.f1
ms.assetid: 26f34f64-f344-486e-9190-acf71aef29a8
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9874b119b634966b146f8fa9d22c016bcd91617b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="azure-hdinsight-pig-task"></a>Azure HDInsight Pig 工作
使用 **Azure HDInsight Pig 工作** ，在 Azure HDInsight 叢集上執行 Pig 指令碼。
     
若要新增 **Azure HDInsight Pig 工作**，請將其拖放至 SSIS 設計師，並按兩下或在其上按一下滑鼠右鍵，然後按一下 [編輯]，即可看到以下 [Azure HDInsight Pig Task Editor (Azure HDInsight Pig 工作編輯器)] 對話方塊。  
  
**Azure HDInsight Pig 工作**是一種元件的[Azure 的 SQL Server Integration Services (SSIS) Feature Pack](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)。
  
 下列清單描述對話方塊中的欄位。  
  
1.  如**HDInsightConnection**欄位中選取現有的 Azure HDInsight 連線管理員，或者建立新的它是指在 Azure HDInsight 叢集的其中一個用來執行指令碼。
  
2.  如**AzureStorageConnection**欄位中選取現有的 Azure 儲存體連線管理員，或者建立新的與叢集相關聯參考 Azure 儲存體帳戶的其中一個。 這是僅有必要，如果您想要下載的指令碼執行輸出和錯誤記錄檔。
 
3.  如**BlobContainer**欄位中，指定與叢集相關聯的儲存體容器名稱。 這是僅有必要，如果您想要下載的指令碼執行輸出和錯誤記錄檔。
  
4.  如**LocalLogFolder**欄位中，指定要將指令碼執行輸出和錯誤記錄檔下載至資料夾。 這是僅有必要，如果您想要下載的指令碼執行輸出和錯誤記錄檔。   
  
5.  有兩種方式可以指定 Pig 指令碼執行：
  
    1.  **內嵌指令碼**： 指定**指令碼**欄位輸入內嵌指令碼中執行**輸入指令碼** 對話方塊。
  
    2.  **指令碼檔案**： 上傳至 Azure Blob 儲存體的指令碼檔案，並指定**BlobName**欄位。 如果 blob 不在預設儲存體帳戶或與 HDInsight 叢集相關聯的容器**ExternalStorageAccountName**和**ExternalBlobContainer**必須指定欄位。 若是外部 blob，請確定它已設定為可公開存取。  
  
     如果同時指定這兩者，就會使用指令碼檔案及內嵌指令碼將會被忽略。

