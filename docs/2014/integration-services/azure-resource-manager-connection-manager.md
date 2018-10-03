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
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a275b540d6199183475298e6a32940ba272f9bc3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48072448"
---
# <a name="azure-resource-manager-connection-manager"></a>Azure Resource Manager 連線管理員
**Azure Resource Manager 連線管理員** 可讓 SSIS 套件使用[服務主體](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal)來管理 Azure 資源。

若要建立及設定 **Azure Resource Manager 連線管理員**，請遵循下列步驟：

1. 在 [新增 SSIS 連線管理員] 對話方塊中，選取 [AzureResourceManager]，然後按一下 [新增]。
2. 在 [Azure Resource Manager Connection Manager Editor] (Azure Resource Manager 連線管理員編輯器) 對話方塊中，指定**應用程式識別碼**、**應用程式金鑰**和**租用戶識別碼**服務主體。 如需這些屬性的詳細資訊，請參閱[這篇](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal)文章。
3. 按一下 **[確定]** ，關閉對話方塊。
4. 您可以在 [屬性]  視窗中看到您建立的連線管理員屬性。
