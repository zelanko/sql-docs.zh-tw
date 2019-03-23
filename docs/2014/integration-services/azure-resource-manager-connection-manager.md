---
title: Azure Resource Manager 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPARMCM.F1
- SQL11.DTS.DESIGNER.AFPARMCM.F1
ms.assetid: a2380258-0418-4a8c-a731-5071a44ddf1e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 55f7aaaa80992240468f3a94d6fd3b9a0f8807b9
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58388526"
---
# <a name="azure-resource-manager-connection-manager"></a>Azure Resource Manager 連線管理員
**Azure Resource Manager 連線管理員** 可讓 SSIS 套件使用[服務主體](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)來管理 Azure 資源。

若要建立及設定 **Azure Resource Manager 連線管理員**，請遵循下列步驟：

1. 在 [新增 SSIS 連線管理員] 對話方塊中，選取 [AzureResourceManager]，然後按一下 [新增]。
2. 在 [Azure Resource Manager Connection Manager Editor] (Azure Resource Manager 連線管理員編輯器) 對話方塊中，指定**應用程式識別碼**、**應用程式金鑰**和**租用戶識別碼**服務主體。 如需這些屬性的詳細資訊，請參閱[這篇](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)文章。
3. 按一下 **[確定]** ，關閉對話方塊。
4. 您可以在 [屬性]  視窗中看到您建立的連線管理員屬性。
