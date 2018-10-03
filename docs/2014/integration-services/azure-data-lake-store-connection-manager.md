---
title: Azure Data Lake Store 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 06/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSCM.F1
- SQL11.DTS.DESIGNER.AFPADLSCM.F1
ms.assetid: 7f1323f9-9dc3-4378-9c70-bbc65bfeabfd
author: yualan
ms.author: douglasl
manager: craigg
ms.openlocfilehash: caba8be6958adf25221b0f81d873b60eb0ee5322
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48172818"
---
# <a name="azure-data-lake-store-connection-manager"></a>Azure Data Lake Store 連線管理員
  **Azure Data Lake Store 連線管理員** 可讓 SSIS 套件透過兩種驗證類型連接到 Azure Data Lake Store 服務︰Azure AD 使用者識別及 Azure AD 服務識別。  

## <a name="configure-the-azure-data-lake-store-connection-manager"></a>設定 Azure Data Lake Store 連線管理員 
  
1.  在 [新增 SSIS 連線管理員]  對話方塊中，選取 [AzureDataLake] ，然後按一下 [新增] 。   
  
2.  在 [Azure Data Lake Store 連線管理員編輯器] 對話方塊中，在 [ADLS Host (ADLS 主機)]  欄位中輸入 Azure Data Lake Store 的主機 URL。 例如： https://test.azuredatalakestore.net或 test.azuredatalakestore.net。
  
3.  選擇對應的驗證類型，以存取 Azure Data Lake Store 資料。

    1.  如已選取 [Azure AD 使用者識別]  驗證選項，請執行下列動作︰

        1. 指定使用者的 [使用者名稱]  和 [密碼]  欄位的值。 
    
        2. 按一下 [測試連接]  按鈕來測試連接。 如果您和您的租用戶系統管理員先前不同意 SSIS 存取您的 Azure Data Lake Store 資料，則需要按一下快顯對話方塊的 [接受]  按鈕，同意 SSIS 存取 Azure Data Lake Store 資料。 如需此同意體驗的詳細資訊，請參閱 [整合應用程式與 Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-integrating-applications#updating-an-application)。
    
        >   [!NOTE] 
        >   [Azure AD 使用者識別] 驗證選項「不」支援多重要素驗證和 Microsoft 帳戶。
    
    2.  如已選取 [Azure AD 服務識別]  驗證選項，請執行下列動作︰
        1. 建立可以存取 Azure Data Lake 資源的 AAD 應用程式和服務主體。
    
        2. 指派此 AAD 應用程式對應的權限以存取 Azure Data Lake 資源。 如需此驗證選項的詳細資訊，請參閱 [Use portal to create Active Directory application and service principal that can access resources](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal)(使用入口網站建立可存取資源的 Active Directory 應用程式和服務主體)。
    
        3. 指定 [用戶端識別碼] 、[祕密金鑰]  和 [租用戶名稱]  欄位的值。
    
        4. 按一下 [測試連接] 按鈕測試連接。  
  
4.  按一下 **[確定]** ，關閉對話方塊。  
  
    您可以在 [屬性]  視窗中看到您建立的連線管理員屬性。  
  
  
