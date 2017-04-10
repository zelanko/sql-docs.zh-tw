---
title: "Azure HDInsight 刪除叢集工作 | Microsoft Docs"
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
  - "sql13.dts.designer.afpdelcltask.f1"
  - "sql14.dts.designer.afpdelcltask.f1"
ms.assetid: e298776e-d18a-4393-a8e6-65ee3d555749
caps.latest.revision: 12
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 9
---
# Azure HDInsight 刪除叢集工作
  **Azure HDInsight 刪除叢集工作**可讓 SSIS 封裝能刪除指定之 Azure 訂用帳戶中的 Azure HDInsight 叢集。  
  
 **Azure HDInsight 刪除叢集工作**是適用於 SQL Server 2016 的 SQL Server Integration Services (SSIS) Feature Pack for Azure 元件。 請在 [這裡](http://go.microsoft.com/fwlink/?LinkID=626967)。  
  
> [!NOTE]  
>  刪除 HDInsight 叢集通常需耗時 10 分鐘。  
  
 若要加入 **Azure HDInsight 刪除叢集工作**，請將其拖放至 SSIS 設計師，並按兩下或在其上按一下滑鼠右鍵，然後按一下 [編輯]，即可看到以下 [Azure HDInsight Delete Cluster Task Editor (Azure HDInsight 刪除叢集工作編輯器)] 對話方塊。  
  
 下表提供對話方塊中欄位的描述。  
  
|||  
|-|-|  
|**欄位**|**說明**|  
|AzureSubscriptionConnection|選取現有 Azure 訂用帳戶連線管理員，或建立參考 Azure 訂用帳戶的新連線管理員，而該訂用帳戶裝載 HDInsight 叢集。|  
|ClusterName|指定要刪除之叢集的名稱。|  
|FailIfNotExists|指定若叢集不存在則工作是否會失敗。|  
  
  