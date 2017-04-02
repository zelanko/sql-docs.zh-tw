---
title: "Azure HDInsight 建立叢集工作 | Microsoft Docs"
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
  - "sql13.dts.designer.afpcreatecltask.f1"
  - "sql14.dts.designer.afpcreatecltask.f1"
ms.assetid: a8ec413a-38d3-45df-887e-6f5f4d9f8465
caps.latest.revision: 11
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Azure HDInsight 建立叢集工作
  [Azure HDInsight Create Cluster Task (Azure HDInsight 建立叢集工作)] 可讓 SSIS 封裝建立指定 Azure 訂用帳戶中的 Azure HDInsight 叢集。  
  
 [Azure HDInsight Create Cluster Task (Azure HDInsight 建立叢集工作)] 是適用於 SQL Server 2016 的 Azure SQL Server Integration Services (SSIS) 功能套件元件。 請在 [這裡](http://go.microsoft.com/fwlink/?LinkID=626967)。  
  
> [!NOTE]  
>  -   建立新的 HDInsight 叢集通常需耗時 10 分鐘。  
> -   建立並執行 Azure HDInsight 叢集並不需要付出任何成本。 如需詳細資料，請參閱 [HDInsight 定價](http://azure.microsoft.com/en-us/pricing/details/hdinsight/)主題。  
  
 若要加入 [Azure HDInsight Create Cluster Task (Azure HDInsight 建立叢集工作)]，請將其拖放至 SSIS 設計師，並按兩下或在其上按一下滑鼠右鍵，然後按一下 [編輯]，即可看到以下 [Azure HDInsight Create Cluster Task Editor (Azure HDInsight 建立叢集工作編輯器)] 對話方塊。  
  
 下表提供此對話方塊中欄位的描述。  
  
|||  
|-|-|  
|**欄位**|**說明**|  
|AzureSubscriptionConnection|選取現有 Azure 訂用帳戶連線管理員，或建立參考 Azure 訂用帳戶的新連線管理員，而該訂用帳戶裝載 HDInsight 叢集。|  
|AzureStorageConnection|選取現有的 Azure 儲存體連線管理員，或建立參考 Azure 儲存體帳戶的新連線管理員，該連線管理員會與 HDInsight 叢集建立關聯。|  
|位置|指定 HDInsight 叢集的位置。 必須在和 Azure 儲存體相同的位置中建立叢集。|  
|ClusterName|指定要建立的 HDInsight 叢集名稱。|  
|ClusterSize|指定您在叢集中想要的節點數目。|  
|BlobContainer|指定與 HDInsight 叢集建立關聯的預設儲存體容器名稱。|  
|UserName|指定具有叢集存取權的使用者名稱。|  
|密碼|指定使用者的密碼。|  
|FailIfExists|指定若叢集已存在則工作是否會失敗。|  
  
> [!NOTE]  
>  HDInsight 叢集與 Azure 儲存體的位置必須相同。  
  
  