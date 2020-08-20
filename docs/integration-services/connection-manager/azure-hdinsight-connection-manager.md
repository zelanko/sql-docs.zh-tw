---
description: Azure HDInsight 連線管理員
title: Azure HDInsight 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPHDICM.F1
- SQL14.DTS.DESIGNER.AFPHDICM.F1
ms.assetid: 29d01bd9-8b38-43b1-b937-67f8aea57c0f
author: Lingxi-Li
ms.author: lingxl
ms.openlocfilehash: 6acb9fec83da610246001df5bc68591ecab1a225
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88478010"
---
# <a name="azure-hdinsight-connection-manager"></a>Azure HDInsight 連線管理員

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


**Azure HDInsight 連線管理員**可讓 SSIS 套件連線到 Azure HDInsight 叢集。

**Azure HDInsight 連線管理員**是 [Azure SQL Server Integration Services (SSIS) Feature Pack](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) 的元件。

若要建立及設定 **Azure HDInsight 連線管理員**，請遵循下列步驟：

1. 在 [新增 SSIS 連線管理員]**** 對話方塊中，選取 [AzureHDInsight]****，然後按一下 [新增]****。
2. 在 [Azure HDInsight Connection Manager Editor] (Azure HDInsight 連線管理員編輯器)**** 對話方塊中，指定 HDInsight 叢集要連線的**叢集 DNS 名稱** (前面不加上通訊協定)、**使用者名稱**和**密碼**。
3. 按一下 **[確定]** ，關閉對話方塊。
4. 您可以在 [屬性] **** 視窗中看到您建立的連線管理員屬性。
