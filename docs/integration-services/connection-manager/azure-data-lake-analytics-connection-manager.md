---
title: Azure Data Lake Analytics Connection Manager | Microsoft Docs
description: SQL Server Integration Services (SSIS) 套件可以使用 Azure Data Lake Analytics 連線管理員連線到 Data Lake Analytics 帳戶。
ms.custom: ''
ms.date: 05/18/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: maghan
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSCM.F1
- sql14.dts.designer.afpadlscm.f1
ms.assetid: f4c44553-0f08-4731-ac47-7534990b8c8d
author: yanancai
ms.author: yanacai
manager: craigg
ms.openlocfilehash: 07470283d3f6028fae4b6435d6134813601009e0
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/22/2019
ms.locfileid: "66012882"
---
# <a name="azure-data-lake-analytics-connection-manager"></a>Azure Data Lake Analytics 連線管理員

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



SQL Server Integration Services (SSIS) 套件可使用 Azure Data Lake Analytics 連線管理員，連線至具有下列兩種驗證類型其中之一的 Data Lake Analytics 帳戶：
-   Azure Active Directory (Azure AD) 使用者身分識別
-   Azure AD 服務識別 

Data Lake Analytics 連線管理員是 [SQL Server Integration Services (SSIS) Feature Pack for Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) 的元件。
 
## <a name="configure-the-connection-manager"></a>設定連線管理員

1. 在 [加入 SSIS 連線管理員]  對話方塊中，選取 [AzureDataLakeAnalytics]  > [加入]。 [Azure Data Lake Analytics Connection Manager 編輯器] 對話方塊隨即開啟。
  
2. 在 [Azure Data Lake Analytics Connection Manager 編輯器] 對話方塊的 [ADLA 帳戶名稱] 欄位中，提供 Data Lake Analytics 帳戶名稱。 例如：myadlaaccountname。
  
3. 在 [驗證] 欄位中，選擇適當的驗證類型來存取 Azure Data Lake Analytics 中的資料。

   A. 如果您選取 [Azure AD 使用者身分識別] 驗證選項：
   
      i. 提供 [使用者名稱] 和 [密碼] 欄位的值。    
      ii. 選取 [測試連線] 來測試連線。 如果您或租用戶系統管理員之前未同意允許 SSIS 存取您的 Data Lake Analytics 帳戶，當提示出現時請選取 [接受]。 如需此同意體驗的詳細資訊，請參閱 [整合應用程式與 Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications#updating-an-application)。
    
   > [!NOTE] 
   > 當您選取 [Azure AD 使用者身分識別] 驗證選項時，不支援多重要素驗證和 Microsoft 帳戶驗證。
    
   B. 如果您選取 [Azure AD 服務身分識別] 驗證選項：
   
      i. 建立 Azure AD 應用程式和服務主體來存取 Data Lake Analytics 帳戶。 如需此驗證選項的詳細資訊，請參閱 [Use portal to create Active Directory application and service principal that can access resources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)(使用入口網站建立可存取資源的 Active Directory 應用程式和服務主體)。    
      ii. 指派合適的權限，讓此 Azure AD 應用程式存取您的 Data Lake Analytics 帳戶。 了解如何[使用新增使用者精靈](https://docs.microsoft.com/azure/data-lake-analytics/data-lake-analytics-manage-use-portal#add-a-new-user)將權限授與 Data Lake Analytics 帳戶。    
      iii. 為 [應用程式識別碼]、[驗證金鑰] 及 [租用戶識別碼] 欄位提供值。    
      iv. 選取 [測試連線] 來測試連線。  

4. 按一下 [確定] 關閉 [Azure Data Lake Analytics Connection Manager 編輯器] 對話方塊。  

## <a name="view-the-properties-of-the-connection-manager"></a>檢視連線管理員的屬性
您可以在 [屬性]  視窗中看到您建立的連線管理員屬性。  
  
  
