---
title: Azure 儲存體連線管理員 | Microsoft Docs
description: Azure 儲存體連線管理員可讓 SSIS 套件連線到 Azure 儲存體帳戶。
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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6d3912e2b5cbf8051348191cf3efb6ed2d20d551
ms.sourcegitcommit: 7183735e38dd94aa3b9bab2b73ccab54c916ff86
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/02/2019
ms.locfileid: "74687197"
---
# <a name="azure-storage-connection-manager"></a>Azure 儲存體連線管理員

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

Azure 儲存體連線管理員可讓 SQL Server Integration Services (SSIS) 套件連線到 Azure 儲存體帳戶。 連線管理員是 [SQL Server Integration Services (SSIS) Feature Pack for Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) 的元件。 
  
在 [加入 SSIS 連線管理員]  對話方塊中，選取 [AzureStorage]   > [加入]  。  
  
有下列屬性可供使用。

- **服務：** 指定要連線的目標儲存體服務。
- **帳戶名稱：** 指定儲存體帳戶名稱。
- **驗證：** 指定要使用的驗證方法。 支援 AccessKey 和 ServicePrincipal 驗證。
    - **AccessKey：** 針對這種驗證方法，指定**帳戶金鑰**。
    - **ServicePrincipal：** 針對此驗證方法，請指定服務主體的**應用程式識別碼**、**應用程式金鑰**和**租用戶識別碼**。
      若要讓**測試連線**正常執行，應將服務主體至少指派給儲存體帳戶的**儲存體 Blob 資料讀者**角色。
      如需詳細資訊，請參閱[在 Azure 入口網站中使用 RBAC 授與 Azure Blob 和佇列資料的存取權](https://docs.microsoft.com/azure/storage/common/storage-auth-aad-rbac-portal#assign-rbac-roles-using-the-azure-portal) \(部分機器翻譯\)。
- **環境：** 指定裝載儲存體帳戶的雲端環境。

## <a name="managed-identities-for-azure-resources-authentication"></a>Azure 資源驗證的受控識別
在 [Azure Data Factory 中的 Azure-SSIS 整合執行階段](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime#azure-ssis-integration-runtime) \(部分機器翻譯\) 上執行 SSIS 套件時，您可以使用與您資料處理站關聯的[受控識別](https://docs.microsoft.com/azure/data-factory/connector-azure-sql-database#managed-identity) \(部分機器翻譯\) 來進行 Azure 儲存體驗證。 指定的處理站可以使用此身分識別從您的儲存體帳戶存取資料，或將資料複製到您的儲存體帳戶。

如需 Azure 儲存體驗證的一般資訊，請參閱[使用 Azure Active Directory 授權存取 Azure Blob 和佇列](https://docs.microsoft.com/azure/storage/common/storage-auth-aad) \(部分機器翻譯\)。 針對 Azure 儲存體使用受控識別驗證：

1. [從 Azure 入口網站尋找資料處理站受控識別](https://docs.microsoft.com/azure/data-factory/data-factory-service-identity)。 前往您資料處理站的**屬性**。 複製 [受控識別應用程式識別碼]  (不是 [受控識別物件識別碼]  )。

1. 在您的儲存體帳戶中將適當權限授與受控識別。 如需角色的詳細資訊，請參閱[使用 RBAC 管理 Azure 儲存體資料的存取權](https://docs.microsoft.com/azure/storage/common/storage-auth-aad-rbac-portal) \(部分機器翻譯\)。

    - 若是存取控制 (IAM) 中的**來源**，至少授與**儲存體 Blob 資料讀者**角色。
    - 若是存取控制 (IAM) 中的**目的地**，至少授與**儲存體 Blob 資料參與者**角色。

接著為 Azure 儲存體連線管理員設定受控識別驗證。 有兩個選項可以執行此操作：

- **在設計階段設定。** 在 [SSIS 設計工具] 中，按兩下 [Azure 儲存體連線管理員] 以開啟 [Azure 儲存體連線管理員編輯器]  。 選取 [在 Azure 上使用受控識別進行驗證]  。
    > [!NOTE]
    >  目前，當您在 SSIS 設計工具中或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server 中執行 SSIS 套件時，此選項不會生效 (表示受控識別驗證無法運作)。
    
- **在執行階段設定。** 當您透過 [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/integration-services/ssis-quickstart-run-ssms) 或 [Azure Data Factory 執行 SSIS 套件活動](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity) \(部分機器翻譯\) 來執行套件時，請尋找 Azure 儲存體連線管理員。 將其屬性 `ConnectUsingManagedIdentity` 更新為 `True`。
    > [!NOTE]
    >  在 Azure-SSIS 整合執行階段中，當受控識別驗證用於儲存體作業時，會覆寫 Azure 儲存體連線管理員上預先設定的所有其他驗證方法 (例如，存取金鑰和服務主體)。

> [!NOTE]
>  若要在現有套件上設定受控識別驗證，建議您使用[最新的 SSIS 設計工具](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)，重建您的 SSIS 專案至少一次。 將該 SSIS 專案重新部署到您的 Azure-SSIS 整合執行階段，以便將新的連線管理員屬性 `ConnectUsingManagedIdentity` 自動加入至 SSIS 專案中的所有 Azure 儲存體連線管理員。 替代方式是在執行階段直接搭配屬性路徑 **\Package.Connections[{您的連線管理員名稱}].Properties[ConnectUsingManagedIdentity]** 使用屬性覆寫。

## <a name="secure-network-traffic-to-your-storage-account"></a>保護目標為您儲存體帳戶的網路流量
Azure Data Factory 現在是 Azure 儲存體的[受信任的 Microsoft 服務](https://docs.microsoft.com/azure/storage/common/storage-network-security#trusted-microsoft-services)。 當您使用受控識別驗證時，可以透過[限制對所選網路的存取](https://docs.microsoft.com/azure/storage/common/storage-network-security#change-the-default-network-access-rule)來保護您的儲存體帳戶，同時仍允許您的資料處理站存取您的儲存體帳戶。 如需指示，請參閱[管理例外狀況](https://docs.microsoft.com/azure/storage/common/storage-network-security#managing-exceptions) \(部分機器翻譯\)。

## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 連接](../../integration-services/connection-manager/integration-services-ssis-connections.md)
