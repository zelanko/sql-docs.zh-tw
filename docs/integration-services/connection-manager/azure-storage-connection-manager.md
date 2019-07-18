---
title: Azure 儲存體連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpstorageconn.f1
- sql14.dts.designer.afpstorageconn.f1
ms.assetid: 68bd1d04-d20f-4357-a34e-7c9c76457062
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 03acf5db82c21a66e2fbd8337713b6989ce36a31
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66403064"
---
# <a name="azure-storage-connection-manager"></a>Azure 儲存體連線管理員

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

  **Azure 儲存體連線管理員**可讓 SSIS 套件連線到 Azure 儲存體帳戶。
   
 **Azure 儲存體連線管理員**是 [Azure SQL Server Integration Services (SSIS) Feature Pack](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) 的元件。 
  
在 [加入 SSIS 連線管理員]  對話方塊中，選取 [AzureStorage]  ，然後按一下 [加入]  。  
  
有下列屬性可供使用。

- **服務：** 指定要連線的目標儲存體服務。
- **帳戶名稱：** 指定儲存體帳戶名稱。
- **驗證：** 指定要使用的驗證方法。 支援 **AccessKey** 和 **ServicePrincipal** 驗證。
    - **AccessKey：** 針對這種驗證方法，指定**帳戶金鑰**。
    - **ServicePrincipal：** 針對這種驗證方法，指定服務主體的**應用程式識別碼**、**應用程式金鑰**、**租用戶識別碼**。
      您應該將儲存體帳戶的**儲存體 Blob 資料參與者**角色指派給服務主體。
      如需詳細資料，請參閱[此](https://docs.microsoft.com/azure/storage/common/storage-auth-aad-rbac-portal#assign-rbac-roles-using-the-azure-portal) \(部分機器翻譯\) 頁面。
- **環境：** 指定裝載儲存體帳戶的雲端環境。
