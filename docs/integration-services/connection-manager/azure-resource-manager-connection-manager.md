---
description: Azure Resource Manager 連線管理員
title: Azure Resource Manager 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPARMCM.F1
- SQL14.DTS.DESIGNER.AFPARMCM.F1
ms.assetid: 8ce8024f-153f-4066-b607-0d36fefc79ed
author: Lingxi-Li
ms.author: lingxl
ms.openlocfilehash: 84b9c97935d0bcf89a4741304bb9a1e6b3576605
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/25/2020
ms.locfileid: "96130137"
---
# <a name="azure-resource-manager-connection-manager"></a>Azure Resource Manager 連線管理員

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


**Azure Resource Manager 連線管理員** 可讓 SSIS 套件使用 [服務主體](/azure/azure-resource-manager/resource-group-create-service-principal-portal)來管理 Azure 資源。

**Azure Resource Manager 連線管理員** 是 [Azure SQL Server Integration Services (SSIS) Feature Pack](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) 的元件。

若要建立及設定 **Azure Resource Manager 連線管理員**，請遵循下列步驟：

1. 在 [新增 SSIS 連線管理員] 對話方塊中，選取 [AzureResourceManager]，然後按一下 [新增]。
2. 在 [Azure Resource Manager Connection Manager Editor] (Azure Resource Manager 連線管理員編輯器) 對話方塊中，指定 **應用程式識別碼**、**應用程式金鑰** 和 **租用戶識別碼** 服務主體。 如需這些屬性的詳細資訊，請參閱[這篇](/azure/azure-resource-manager/resource-group-create-service-principal-portal)文章。
3. 按一下 [確定]  關閉對話方塊。
4. 您可以在 [屬性]  視窗中看到您建立的連線管理員屬性。