---
title: "Azure HDInsight 建立叢集工作 |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 02/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.afpcreatecltask.f1
- sql14.dts.designer.afpcreatecltask.f1
ms.assetid: a8ec413a-38d3-45df-887e-6f5f4d9f8465
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 71a24dc15253916c32b07e6024e2ab32514c9d39
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="azure-hdinsight-create-cluster-task"></a>Azure HDInsight 建立叢集工作
**Azure HDInsight 建立叢集工作**可讓 SSIS 封裝在指定的 Azure 訂用帳戶和資源群組中建立的 Azure HDInsight 叢集。
  
**Azure HDInsight 建立叢集工作**是一種元件的[Azure 的 SQL Server Integration Services (SSIS) Feature Pack](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)。
  
> [!NOTE]  
> - 建立新的 HDInsight 叢集可能需要 10 ~ 20 分鐘。  
> - 沒有與建立和執行 Azure HDInsight 叢集相關聯的成本。 請參閱[HDInsight 定價](http://azure.microsoft.com/en-us/pricing/details/hdinsight/)如需詳細資訊。  
  
若要加入 [Azure HDInsight Create Cluster Task (Azure HDInsight 建立叢集工作)]，請將其拖放至 SSIS 設計師，並按兩下或在其上按一下滑鼠右鍵，然後按一下 [編輯]，即可看到以下 [Azure HDInsight Create Cluster Task Editor (Azure HDInsight 建立叢集工作編輯器)] 對話方塊。  
  
下表提供此對話方塊中欄位的描述。  
  
|||  
|-|-|  
|**欄位**|**說明**|  
|AzureResourceManagerConnection|選取現有的 Azure 資源管理員的連接管理員或建立可用於建立 HDInsight 叢集的新連線。|  
|AzureStorageConnection|選取現有的 Azure 儲存體連線管理員，或建立參考 Azure 儲存體帳戶的新連線管理員，該連線管理員會與 HDInsight 叢集建立關聯。|
|訂用帳戶 Id|指定 HDInsight 叢集會在中建立的訂用帳戶 ID。|
|資源群組|指定 Azure 資源群組的 HDInsight 叢集會在中建立。|
|位置|指定 HDInsight 叢集的位置。 必須指定 Azure 儲存體帳戶的相同位置中建立叢集。|  
|ClusterName|指定要建立的 HDInsight 叢集名稱。|  
|ClusterSize|指定要在叢集中建立節點的數目。|  
|BlobContainer|指定要與 HDInsight 叢集相關聯的預設儲存體容器名稱。|  
|UserName|指定要用來連接到 HDInsight 叢集的使用者名稱。|  
|密碼|指定要用來連接到 HDInsight 叢集的密碼。|
|SshUserName|指定用來從遠端存取使用 SSH 的 HDInsight 叢集的使用者名稱。|
|SshPassword|指定用來從遠端存取使用 SSH 的 HDInsight 叢集的密碼。|
|FailIfExists|指定若叢集已存在則工作是否會失敗。|  
  
> [!NOTE]  
> HDInsight 叢集和 Azure 儲存體帳戶的位置必須相同。

