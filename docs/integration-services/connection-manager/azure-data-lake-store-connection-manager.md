---
title: "Azure Data Lake Store 連接管理員 |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: douglasl
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSCM.F1
- sql14.dts.designer.afpadlscm.f1
ms.assetid: f4c44553-0f08-4731-ac47-7534990b8c8d
caps.latest.revision: 7
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 29b296b2ae7e04871e81a9c236cb990bdd19562b
ms.openlocfilehash: 0a84b10114d785c9216a0902b2eefbcb0bd3f4c8
ms.contentlocale: zh-tw
ms.lasthandoff: 10/11/2017

---
# <a name="azure-data-lake-store-connection-manager"></a>Azure Data Lake Store 連線管理員
SQL Server Integration Services (SSIS) 封裝可使用 Azure 資料湖存放區連接管理員來連接至 Azure Data Lake Store 服務具有下列其中一種下列驗證：
-   Azure AD 使用者的身分識別
-   Azure AD 服務身分識別 

Azure Data Lake Store 連接管理員是元件[Azure 的 SQL Server Integration Services (SSIS) Feature Pack](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)。

>   [!NOTE]
> 為確保 Azure Data Lake Store 連線管理員及使用它的元件 (即 Azure Data Lake Store 來源及 Azure Data Lake Store 目的地) 能夠連接服務，請務必從 [這裡](https://www.microsoft.com/download/details.aspx?id=49492)下載最新版的 Azure Feature Pack。 
 
## <a name="configure-the-azure-data-lake-store-connection-manager"></a>設定 Azure Data Lake Store 連線管理員

1.  在**加入 SSIS 連接管理員**對話方塊中，選取**AzureDataLake**，然後選取**新增**。 **Azure 資料湖存放區連接管理員編輯器**對話方塊隨即開啟。
  
2.  在**Azure 資料湖存放區連接管理員編輯器**對話方塊中，於**ADLS 主機**欄位中提供的 Azure Data Lake Store 主機 URL。 例如：`https://test.azuredatalakestore.net`或`test.azuredatalakestore.net`。
  
3.  在**驗證**欄位中，選擇適當的驗證類型來存取 Azure 資料湖存放區中的資料。

    1.  如果您選取**Azure AD 使用者的身分識別**驗證選項，請執行下列動作：
        1. 提供的值**使用者名**和**密碼**欄位。 
    
        2. 若要測試連線，請選取**測試連接**。 如果您或租用戶系統管理員先前未同意以允許存取您的 Azure 資料湖存放區資料，請選取 SSIS**接受**出現提示時。 如需此同意體驗的詳細資訊，請參閱 [整合應用程式與 Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-integrating-applications#updating-an-application)。
    
        >   [!NOTE] 
        > 當您選取**Azure AD 使用者的身分識別**不支援的驗證選項、 多因素驗證和 Microsoft 帳戶驗證。
    
    2. 如果您選取**Azure AD 服務身分識別**驗證選項，請執行下列動作：
        1. 建立 Azure Active Directory (AAD) 應用程式和服務主體以存取 Azure 資料湖資料。
    
        2. 指派適當的權限，讓此 AAD 應用程式存取您的 Azure 資料湖資源。 如需此驗證選項的詳細資訊，請參閱 [Use portal to create Active Directory application and service principal that can access resources](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal)(使用入口網站建立可存取資源的 Active Directory 應用程式和服務主體)。
    
        3. 提供的值**用戶端識別碼**，**秘密金鑰**，和**租用戶名稱**欄位。
    
        4. 若要測試連線，請選取**測試連接**。  
  
6.  選取**確定**關閉**Azure 資料湖存放區連接管理員編輯器** 對話方塊。  

## <a name="view-the-properties-of-the-connection-manager"></a>檢視連接管理員的屬性
您可以在 [屬性]  視窗中看到您建立的連線管理員屬性。  
  
  

