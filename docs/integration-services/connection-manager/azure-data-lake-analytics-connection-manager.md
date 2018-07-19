---
title: Azure Data Lake Analytics Connection Manager | Microsoft Docs
ms.custom: ''
ms.date: 05/18/2018
ms.prod: sql
ms.prod_service: integration-services
ms.component: connection-manager
ms.reviewer: douglasl
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSCM.F1
- sql14.dts.designer.afpadlscm.f1
ms.assetid: f4c44553-0f08-4731-ac47-7534990b8c8d
caps.latest.revision: 7
author: yanancai
ms.author: yanacai
manager: craigg
ms.openlocfilehash: 17b63aad55cf50262d7e1e56267859b1a34cc9d3
ms.sourcegitcommit: 44e9bf62f2c75449c17753ed66bf85c43928dbd5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/05/2018
ms.locfileid: "37854404"
---
# <a name="azure-data-lake-analytics-connection-manager"></a>Azure Data Lake Analytics Connection Manager

SQL Server Integration Services (SSIS) 套件可使用 Azure Data Lake Analytics 連線管理員，連線至具有下列兩種驗證類型其中之一的 Azure Data Lake Analytics 帳戶：
-   Azure AD 使用者身分識別
-   Azure AD 服務識別 

Azure Data Lake Analytics 連線管理員是 [SQL Server Integration Services (SSIS) Feature Pack for Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) 的元件。
 
## <a name="configure-the-azure-data-lake-analytics-connection-manager"></a>設定 Azure Data Lake Analytics Connection Manager

1.  在 [新增 SSIS 連線管理員] 對話方塊中，選取 [AzureDataLakeAnalytics]，然後選取 [新增]。 [Azure Data Lake Analytics Connection Manager 編輯器] 對話方塊隨即開啟。
  
2.  在 [Azure Data Lake Analytics Connection Manager 編輯器] 對話方塊的 [ADLA 帳戶] 欄位中，提供 Azure Data Lake Analytics 帳戶名稱。 例如：myadlaaccountname。
  
3.  在 [驗證] 欄位中，選擇適當的驗證類型來存取 Azure Data Lake Analytics 中的資料。

    1.  如果選取 [Azure AD 使用者身分識別] 驗證選項，請執行下列動作︰
        1. 提供 [使用者名稱] 和 [密碼] 欄位的值。 
    
        2. 選取 [測試連線] 來測試連線。 如果您或租用戶系統管理員之前未同意允許 SSIS 存取您的 Azure Data Lake Analytics 帳戶，當提示出現時請選取 [接受]。 如需此同意體驗的詳細資訊，請參閱[整合應用程式與 Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications#updating-an-application)。
    
        >   [!NOTE] 
        > 當您選取 [Azure AD 使用者身分識別] 驗證選項時，不支援多重要素驗證和 Microsoft 帳戶驗證。
    
    2. 如果選取 [Azure AD 服務識別] 驗證選項，請執行下列動作︰
        1. 建立 Azure Active Directory (AAD) 應用程式和服務主體以存取 Azure Data Lake Analytics 帳戶。 如需此驗證選項的詳細資訊，請參閱 [Use portal to create Active Directory application and service principal that can access resources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal) (使用入口網站建立可存取資源的 Active Directory 應用程式和服務主體)。
    
        2. 指派合適的權限，讓此 AAD 應用程式存取 Azure Data Lake Analytics 帳戶。 了解如何[使用新增使用者精靈](https://docs.microsoft.com/azure/data-lake-analytics/data-lake-analytics-manage-use-portal#add-a-new-user)將權限授與 Azure Data Lake Analytics 帳戶。 
    
        3. 為 [應用程式識別碼]、[驗證金鑰] 及 [租用戶識別碼] 欄位提供值。
    
        4. 選取 [測試連線] 來測試連線。  

4.  按一下 [確定] 關閉 [Azure Data Lake Analytics Connection Manager 編輯器] 對話方塊。  

## <a name="view-the-properties-of-the-connection-manager"></a>檢視連線管理員的屬性
您可以在 [屬性]  視窗中看到您建立的連線管理員屬性。  
  
  
