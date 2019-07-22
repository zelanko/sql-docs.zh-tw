---
title: Azure Data Lake Store 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: maghan
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSCM.F1
- sql14.dts.designer.afpadlscm.f1
ms.assetid: f4c44553-0f08-4731-ac47-7534990b8c8d
author: Lingxi-Li
ms.author: lingxl
ms.openlocfilehash: 095865071b3a9ddfcba15635d9e3d857b2dbee20
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67904788"
---
# <a name="azure-data-lake-store-connection-manager"></a>Azure Data Lake Store 連線管理員

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


SQL Server Integration Services (SSIS) 套件可以使用 Azure Data Lake Store 連線管理員，連線至具有下列兩種驗證類型之一的 Azure Data Lake Storage Gen1 帳戶：
-   Azure AD 使用者身分識別
-   Azure AD 服務識別 

Azure Data Lake Store 連線管理員是 [SQL Server Integration Services (SSIS) Feature Pack for Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) 的元件。

> [!NOTE]
> 為確保 Azure Data Lake Store 連線管理員以及使用它的元件 (即 Data Lake Storage Gen1 來源和 Data Lake Storage Gen1 目的地) 能夠連線服務，請務必從[這裡](https://www.microsoft.com/download/details.aspx?id=49492)下載最新版的 Azure Feature Pack。 
 
## <a name="configure-the-azure-data-lake-store-connection-manager"></a>設定 Azure Data Lake Store 連線管理員

1.  在 [新增 SSIS 連線管理員]  對話方塊中，選取 [AzureDataLake]  ，然後選取 [新增]  。 [Azure Data Lake Store Connection Manager Editor] (Azure Data Lake Store 連線管理員編輯器)  對話方塊隨即開啟。
  
2.  在 [Azure Data Lake Store Connection Manager Editor] (Azure Data Lake Store 連線管理員編輯器)  對話方塊的 [ADLS Host] \(ADLS 主機\)  欄位中，提供 Data Lake Storage Gen1 主機 URL。 例如：`https://test.azuredatalakestore.net` 或 `test.azuredatalakestore.net`。
  
3.  在 [驗證]  欄位中，選擇適當的驗證類型來存取 Data Lake Storage Gen1 中的資料。

    1.  如果選取 [Azure AD 使用者身分識別]  驗證選項，請執行下列動作︰
        1. 提供 [使用者名稱]  和 [密碼]  欄位的值。 
    
        2. 選取 [測試連線]  來測試連線。 如果您或租用戶系統管理員之前未同意允許 SSIS 存取您的 Data Lake Storage Gen1 資料，因此當提示出現時請選取 [接受]  。 如需此同意體驗的詳細資訊，請參閱 [整合應用程式與 Azure Active Directory](https://docs.microsoft.com/azure/active-directory/manage-apps/plan-an-application-integration#integrating-applications-with-azure-ad)。
    
        > [!NOTE] 
        > 當您選取 [Azure AD 使用者身分識別]  驗證選項時，不支援多重要素驗證和 Microsoft 帳戶驗證。
    
    2. 如果選取 [Azure AD 服務識別]  驗證選項，請執行下列動作︰
        1. 建立 Azure Active Directory (AAD) 應用程式和服務主體以存取 Data Lake Storage Gen1 資料。
    
        2. 指派合適的權限，讓此 AAD 應用程式存取 Data Lake Storage Gen1 資源。 如需此驗證選項的詳細資訊，請參閱 [Use portal to create Active Directory application and service principal that can access resources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)(使用入口網站建立可存取資源的 Active Directory 應用程式和服務主體)。
    
        3. 提供 [用戶端識別碼]  、[祕密金鑰]  和 [租用戶名稱]  欄位的值。
    
        4. 選取 [測試連線]  來測試連線。  
  
6.  按一下 [確定]  關閉 [Azure Data Lake Store Connection Manager Editor] (Azure Data Lake Store 連線管理員編輯器)  對話方塊。  

## <a name="view-the-properties-of-the-connection-manager"></a>檢視連線管理員的屬性
您可以在 [屬性]  視窗中看到您建立的連線管理員屬性。  
  
  
