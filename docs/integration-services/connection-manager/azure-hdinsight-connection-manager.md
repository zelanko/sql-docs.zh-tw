---
title: "Azure HDInsight 連線管理員 | Microsoft Docs"
ms.custom: 
ms.date: 02/28/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPHDICM.F1
- SQL14.DTS.DESIGNER.AFPHDICM.F1
ms.assetid: 29d01bd9-8b38-43b1-b937-67f8aea57c0f
caps.latest.revision: "4"
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3f355976dfdf595cfe152d15579fa546940a5562
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="azure-hdinsight-connection-manager"></a>Azure HDInsight 連線管理員
**Azure HDInsight 連線管理員**可讓 SSIS 套件連線到 Azure HDInsight 叢集。

**Azure HDInsight 連線管理員**是 [Azure SQL Server Integration Services (SSIS) Feature Pack](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) 的元件。

若要建立及設定 **Azure HDInsight 連線管理員**，請遵循下列步驟：

1. 在 [新增 SSIS 連線管理員] 對話方塊中，選取 [AzureHDInsight]，然後按一下 [新增]。
2. 在 [Azure HDInsight Connection Manager Editor] (Azure HDInsight 連線管理員編輯器) 對話方塊中，指定 HDInsight 叢集要連線的**叢集 DNS 名稱** (前面不加上通訊協定)、**使用者名稱**和**密碼**。
3. 按一下 **[確定]** ，關閉對話方塊。
4. 您可以在 [屬性]  視窗中看到您建立的連線管理員屬性。
