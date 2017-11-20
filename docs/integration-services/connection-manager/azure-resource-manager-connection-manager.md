---
title: "Azure 資源管理員的連線管理員 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPARMCM.F1
- SQL14.DTS.DESIGNER.AFPARMCM.F1
ms.assetid: 8ce8024f-153f-4066-b607-0d36fefc79ed
caps.latest.revision: 3
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: dd1dbf668bf3ac24d9d6598b0ff9e2256d897c42
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="azure-resource-manager-connection-manager"></a>Azure 資源管理員的連接管理員
**Azure 資源管理員的連線管理員**讓 SSIS 封裝來管理 Azure 資源使用[服務主體](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal)。

**Azure 資源管理員的連線管理員**是一種元件的[Azure 的 SQL Server Integration Services (SSIS) Feature Pack](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)。

若要建立及設定**Azure 資源管理員的連線管理員**，依照下列步驟：

1. 在**加入 SSIS 連接管理員**對話方塊中，選取**AzureResourceManager**，然後按一下**新增**。
2. 在**Azure 資源管理員的連接管理員編輯器**對話方塊方塊中，指定**應用程式識別碼**，**應用程式金鑰**，和**租用戶識別碼**服務主體。 如需有關這些屬性的詳細資訊，請參閱[這](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal)發行項。
3. 按一下 **[確定]** ，關閉對話方塊。
4. 您可以在 [屬性]  視窗中看到您建立的連線管理員屬性。

