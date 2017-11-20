---
title: "Azure HDInsight 刪除叢集工作 |Microsoft 文件"
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
- sql13.dts.designer.afpdelcltask.f1
- sql14.dts.designer.afpdelcltask.f1
ms.assetid: e298776e-d18a-4393-a8e6-65ee3d555749
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f98b69e8bd3b2e78f6dd20a19ca17a83a834c3b3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="azure-hdinsight-delete-cluster-task"></a>Azure HDInsight 刪除叢集工作
**Azure HDInsight 刪除叢集工作**讓 SSIS 封裝能刪除指定的 Azure 訂用帳戶和資源群組中的 Azure HDInsight 叢集。
  
**Azure HDInsight 刪除叢集工作**是一種元件的[Azure 的 SQL Server Integration Services (SSIS) Feature Pack](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)。
  
> [!NOTE]
> 刪除 HDInsight 叢集可能需要 10 ~ 20 分鐘。  
  
若要加入 **Azure HDInsight 刪除叢集工作**，請將其拖放至 SSIS 設計工具，並按兩下或在其上按一下滑鼠右鍵，然後按一下 [編輯]  ，即可看到以下 [Azure HDInsight 刪除叢集工作編輯器]  對話方塊。  
  
下表提供對話方塊中欄位的描述。  
  
|||  
|-|-|  
|**欄位**|**說明**|  
|AzureResourceManagerConnection|選取現有的 Azure 資源管理員的連接管理員或建立將用來刪除 HDInsight 叢集的新連線。|
|訂用帳戶 Id|指定 HDInsight 叢集位於訂用帳戶 ID。|
|資源群組|指定 HDInsight 叢集位於 Azure 資源群組。|
|ClusterName|指定要刪除之叢集的名稱。|  
|FailIfNotExists|指定若叢集不存在則工作是否會失敗。|

