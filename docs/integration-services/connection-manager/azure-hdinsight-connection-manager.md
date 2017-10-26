---
title: "Azure HDInsight 連線管理員 |Microsoft 文件"
ms.custom: 
ms.date: 02/28/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPHDICM.F1
- SQL14.DTS.DESIGNER.AFPHDICM.F1
ms.assetid: 29d01bd9-8b38-43b1-b937-67f8aea57c0f
caps.latest.revision: 4
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 080cd1184d3c29673ac476d6fe6087b697160544
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="azure-hdinsight-connection-manager"></a>Azure HDInsight 連線管理員
**Azure HDInsight 連線管理員**可讓 SSIS 封裝連接到 Azure HDInsight 叢集。

**Azure HDInsight 連線管理員**是一種元件的[Azure 的 SQL Server Integration Services (SSIS) Feature Pack](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)。

若要建立及設定**Azure HDInsight 連線管理員**，依照下列步驟：

1. 在**加入 SSIS 連接管理員**對話方塊中，選取**AzureHDInsight**，然後按一下**新增**。
2. 在**Azure HDInsight 連線管理員編輯器**對話方塊方塊中，指定**叢集 DNS 名稱**（不含通訊協定前置詞）， **Username**，和**密碼**連接到 HDInsight 叢集。
3. 按一下 **[確定]** ，關閉對話方塊。
4. 您可以在 [屬性]  視窗中看到您建立的連線管理員屬性。

