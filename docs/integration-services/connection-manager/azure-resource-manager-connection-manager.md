---
title: "Azure Resource Manager 連線管理員 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
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
- SQL13.DTS.DESIGNER.AFPARMCM.F1
- SQL14.DTS.DESIGNER.AFPARMCM.F1
ms.assetid: 8ce8024f-153f-4066-b607-0d36fefc79ed
caps.latest.revision: "3"
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 478125f9c60093a49682d709d77d3b196bd53938
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/01/2017
---
# <a name="azure-resource-manager-connection-manager"></a>Azure Resource Manager 連線管理員
**Azure Resource Manager 連線管理員** 可讓 SSIS 套件使用[服務主體](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)來管理 Azure 資源。

**Azure Resource Manager 連線管理員**是 [Azure SQL Server Integration Services (SSIS) Feature Pack](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) 的元件。

若要建立及設定 **Azure Resource Manager 連線管理員**，請遵循下列步驟：

1. 在 [新增 SSIS 連線管理員] 對話方塊中，選取 [AzureResourceManager]，然後按一下 [新增]。
2. 在 [Azure Resource Manager Connection Manager Editor] (Azure Resource Manager 連線管理員編輯器) 對話方塊中，指定**應用程式識別碼**、**應用程式金鑰**和**租用戶識別碼**服務主體。 如需這些屬性的詳細資訊，請參閱[這篇](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)文章。
3. 按一下 **[確定]** ，關閉對話方塊。
4. 您可以在 [屬性]  視窗中看到您建立的連線管理員屬性。
