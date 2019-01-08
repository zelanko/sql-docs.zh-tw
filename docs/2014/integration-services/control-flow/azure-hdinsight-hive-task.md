---
title: Azure HDInsight Hive 工作 | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afphivetask.f1
- sql11.dts.designer.afphivetask.f1
ms.assetid: e1896c73-128a-4128-9814-3e01f7dfe19b
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ef43e6539840e6c5eec68ad4911f72930d28591d
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52749490"
---
# <a name="azure-hdinsight-hive-task"></a>Azure HDInsight Hive 工作
使用 **Azure HDInsight Hive 工作**，在 Azure HDInsight 叢集上執行 Hive 指令碼。
     
若要新增 **Azure HDInsight Hive 工作**，請將其拖放至 SSIS 設計師，並按兩下或在其上按一下滑鼠右鍵，然後按一下 [編輯]，即可看到以下 [Azure HDInsight Hive Task Editor (Azure HDInsight Hive 工作編輯器)] 對話方塊。  
  
 下列清單描述對話方塊中的欄位。  
  
1.  針對 [HDInsightConnection] 欄位，選取現有的 Azure HDInsight 連線管理員或建立新的連線管理員，以參考用來執行指令碼的 Azure HDInsight 叢集。
  
2.  針對 [AzureStorageConnection] 欄位，選取現有的 Azure 儲存體連線管理員或建立新的連線管理員，以參考與叢集相關聯的 Azure 儲存體帳戶。 只有在您想要下載指令碼執行輸出和錯誤記錄檔時才需要此欄位。
 
3.  針對 [BlobContainer] 欄位，指定與叢集相關聯的儲存體容器名稱。 只有在您想要下載指令碼執行輸出和錯誤記錄檔時才需要此欄位。
  
4.  針對 [LocalLogFolder] 欄位，指定要下載指令碼執行輸出和錯誤記錄檔的目標資料夾。 只有在您想要下載指令碼執行輸出和錯誤記錄檔時才需要此欄位。   
  
5.  有兩個方法可以指定要執行的 Hive 指令碼：
  
    1.  **內嵌指令碼**:指定**指令碼**輸入欄位中內嵌指令碼中執行**輸入指令碼** 對話方塊。
  
    2.  **指令碼檔案**:將指令碼檔案上傳至 Azure Blob 儲存體，並指定**BlobName**欄位。 如果 blob 不在與 HDInsight 叢集相關聯的預設儲存體帳戶或容器中，則必須指定 [ExternalStorageAccountName] 和 [ExternalBlobContainer] 欄位。 若是外部 blob，請確定它已設定為可公開存取。  
  
     如果指定兩者，則會使用指令檔並忽略內嵌指令碼。
