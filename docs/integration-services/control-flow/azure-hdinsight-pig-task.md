---
title: Azure HDInsight Pig 工作 | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afppigtask.f1
- sql14.dts.designer.afppigtask.f1
ms.assetid: 26f34f64-f344-486e-9190-acf71aef29a8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 44d6fd9052b2f36381b95223222ec9008a8e4728
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298408"
---
# <a name="azure-hdinsight-pig-task"></a>Azure HDInsight Pig 工作

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


使用 **Azure HDInsight Pig 工作** ，在 Azure HDInsight 叢集上執行 Pig 指令碼。
     
若要新增 **Azure HDInsight Pig 工作**，請將其拖放至 SSIS 設計師，並按兩下或在其上按一下滑鼠右鍵，然後按一下 [編輯]  ，即可看到以下 [Azure HDInsight Pig Task Editor (Azure HDInsight Pig 工作編輯器)]  對話方塊。  
  
**Azure HDInsight Pig 工作** 是 [Azure SQL Server Integration Services (SSIS) Feature Pack](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) 的元件。
  
 下列清單描述對話方塊中的欄位。  
  
1.  針對 [HDInsightConnection]  欄位，選取現有的 Azure HDInsight 連線管理員或建立新的連線管理員，以參考用來執行指令碼的 Azure HDInsight 叢集。
  
2.  針對 [AzureStorageConnection]  欄位，選取現有的 Azure 儲存體連線管理員或建立新的連線管理員，以參考與叢集相關聯的 Azure 儲存體帳戶。 只有在您想要下載指令碼執行輸出和錯誤記錄檔時才需要此欄位。
 
3.  針對 [BlobContainer]  欄位，指定與叢集相關聯的儲存體容器名稱。 只有在您想要下載指令碼執行輸出和錯誤記錄檔時才需要此欄位。
  
4.  針對 [LocalLogFolder]  欄位，指定要下載指令碼執行輸出和錯誤記錄檔的目標資料夾。 只有在您想要下載指令碼執行輸出和錯誤記錄檔時才需要此欄位。   
  
5.  有兩個方法可以指定要執行的 Pig 指令碼：
  
    1.  **內嵌指令碼**：透過在 [輸入指令碼]  對話方塊中輸入要執行的內嵌指令碼，來指定 [指令碼]  欄位。
  
    2.  **指令檔**：將指令檔上傳至 Azure Blob 儲存體，並指定 **BlobName** 欄位。 如果 blob 不在與 HDInsight 叢集相關聯的預設儲存體帳戶或容器中，則必須指定 [ExternalStorageAccountName]  和 [ExternalBlobContainer]  欄位。 若是外部 blob，請確定它已設定為可公開存取。  
  
     如果指定兩者，則會使用指令檔並忽略內嵌指令碼。
