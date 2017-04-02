---
title: "Azure HDInsight Hive 工作 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "02/28/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.afphivetask.f1"
  - "sql14.dts.designer.afphivetask.f1"
ms.assetid: e1896c73-128a-4128-9814-3e01f7dfe19b
caps.latest.revision: 13
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# Azure HDInsight Hive 工作
  使用 **Azure HDInsight Hive 工作**，在 Azure HDInsight 叢集上執行 Hive 指令碼。
     
若要新增 **Azure HDInsight Hive 工作**，請將其拖放至 SSIS 設計師，並按兩下或在其上按一下滑鼠右鍵，然後按一下 [編輯]，即可看到以下 [Azure HDInsight Hive Task Editor (Azure HDInsight Hive 工作編輯器)] 對話方塊。  
  
 **Azure HDInsight Hive 工作**是適用於 SQL Server 2016 的 SQL Server Integration Services (SSIS) Feature Pack for Azure 元件。 請在 [這裡](http://go.microsoft.com/fwlink/?LinkID=626967)。  
  
 下列清單描述對話方塊中的欄位。  
  
1.  針對 [AzureSubscriptionConnection]  欄位選取現有 Azure 訂用帳戶連接管理員，或建立參考 Azure 訂用帳戶的新連接管理員，而該訂用帳戶裝載 HDInsight 叢集。  
  
2.  針對 **HDInsightClusterName** 欄位選取您要在其上執行 Hive 指令碼之 HDInsight 叢集的名稱。  
  
3.  針對 [LocalLogFolder] 欄位，按一下 [... (省略符號)]，然後選取您要從 HDInsight 叢集下載 Hive 處理記錄的目標資料夾。  
  
4.  有兩個方法可以指定 Hive 指令碼：  
  
    1.  **內嵌指令碼**︰按一下 [指令碼] 欄位旁的 [... (省略符號)]，然後在 [輸入指令碼] 對話方塊中輸入內嵌指令碼。  
  
    2.  **指令碼檔案**︰將指令碼檔案上傳至 Blob 位置，並指定其 **BlobName**。 如果 Blob 不在 HDInsight 叢集的預設儲存體或容器中，則必須指定 **ExternalStorageAccountName** 和 **ExternalBlobContainer** 。 若是外部 Blob，請確定它已設定為可公用存取。  
  
     如果指定兩者，則會使用指令碼檔案並忽略內嵌指令碼。  
  
  