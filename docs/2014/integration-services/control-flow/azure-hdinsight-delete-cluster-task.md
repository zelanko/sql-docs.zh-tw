---
title: Azure HDInsight 刪除叢集工作 | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.afpdelcltask.f1
- sql11.dts.designer.afpdelcltask.f1
ms.assetid: e298776e-d18a-4393-a8e6-65ee3d555749
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 42a7a3d89d4f8c939e097cdb9016f2be7b0e35d7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36144976"
---
# <a name="azure-hdinsight-delete-cluster-task"></a>Azure HDInsight 刪除叢集工作
**Azure HDInsight 刪除叢集工作**可讓 SSIS 套件刪除指定之 Azure 訂用帳戶和資源群組中的 Azure HDInsight 叢集。
  
> [!NOTE]
> 刪除 HDInsight 叢集可能需要 10~20 分鐘。  
  
若要加入 **Azure HDInsight 刪除叢集工作**，請將其拖放至 SSIS 設計工具，並按兩下或在其上按一下滑鼠右鍵，然後按一下 [編輯]  ，即可看到以下 [Azure HDInsight 刪除叢集工作編輯器]  對話方塊。  
  
下表提供此對話方塊中欄位的描述。  
  
|||  
|-|-|  
|**欄位**|**說明**|  
|AzureResourceManagerConnection|選取現有的 Azure Resource Manager 連線管理員或建立新的連線管理員，以用來刪除 HDInsight 叢集。|
|SubscriptionId|指定 HDInsight 叢集所在的訂用帳戶 ID。|
|ResourceGroup|指定 HDInsight 叢集所在的 Azure 資源群組。|
|ClusterName|指定要刪除之叢集的名稱。|  
|FailIfNotExists|指定若叢集不存在則工作是否會失敗。|