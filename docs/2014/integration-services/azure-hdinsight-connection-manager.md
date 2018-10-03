---
title: Azure HDInsight 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPHDICM.F1
- SQL11.DTS.DESIGNER.AFPHDICM.F1
ms.assetid: 850a978d-5dba-45b6-a10e-306aafbc353d
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d3995c1b0f830277441e236d375c87f21f8d42f8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48221908"
---
# <a name="azure-hdinsight-connection-manager"></a>Azure HDInsight 連線管理員
**Azure HDInsight 連線管理員**可讓 SSIS 套件連線到 Azure HDInsight 叢集。

若要建立及設定 **Azure HDInsight 連線管理員**，請遵循下列步驟：

1. 在 [新增 SSIS 連線管理員] 對話方塊中，選取 [AzureHDInsight]，然後按一下 [新增]。
2. 在 [Azure HDInsight Connection Manager Editor] (Azure HDInsight 連線管理員編輯器) 對話方塊中，指定 HDInsight 叢集要連線的**叢集 DNS 名稱** (前面不加上通訊協定)、**使用者名稱**和**密碼**。
3. 按一下 **[確定]** ，關閉對話方塊。
4. 您可以在 [屬性]  視窗中看到您建立的連線管理員屬性。
