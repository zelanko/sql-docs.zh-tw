---
title: 第 1 課：建立和套用 Off By Default 原則 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: d31367db-b7db-44c4-8df2-f1240474cf78
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: b5d665bc5f97bf43c74bbe2f24875c3917b139f3
ms.sourcegitcommit: ef6e3ec273b0521e7c79d5c2a4cb4dcba1744e67
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/10/2018
ms.locfileid: "51512713"
---
# <a name="lesson-1-create-and-apply-an-off-by-default-policy"></a>第 1 課：建立和套用 Off By Default 原則
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
您可以使用以原則為基礎的管理原則來管理一個或多個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體、一個或多個執行個體物件、伺服器執行個體、一個或多個資料庫或一個或多個資料庫物件。 身為資料庫管理員，您想要確保特定伺服器沒有啟用 Database Mail。 在這一課，您將建立一個條件，以及設定這個伺服器選項的原則。 您將會測試伺服器，以便查看它是否符合此原則。 然後，您將會使用此原則來重新設定伺服器，以便讓伺服器符合。  

## <a name="prerequisites"></a>Prerequisites
若要完成本教學課程，您需要 SQL Server Management Studio 和執行 SQL Server 的伺服器存取權。 

- 安裝 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
- 安裝 [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)。
  
## <a name="create-the-mail-off-condition"></a>建立 mail-off 條件

1.  在物件總管中，依序展開 [管理]、[原則管理] 和 [Facet]、以滑鼠右鍵按一下 [介面區組態]，然後按一下 [新增條件]。  

    ![新增條件](Media/lesson-1-create-and-apply-an-off-by-default-policy/new-surface-area-condition.png)
  
2.  在 [建立新條件] 對話方塊的 [名稱] 方塊中，輸入 **Mail Off**。   
    1. 在 [Facet] 方塊中，確認已選取 [介面區組態] Facet。
    1. 在 [運算式] 區域的 [欄位] 方塊中，選取 [@DatabaseMailEnabled]、在 [運算子] 方塊中選取 [=]，然後在 [值] 中選取 [False]。  
    1. 在 [描述] 頁面上，輸入條件的描述，然後按一下 [確定] 建立條件。  

    ![Mail off 條件](Media/lesson-1-create-and-apply-an-off-by-default-policy/mail-off-condition.png) 
  
## <a name="create-the-off-by-default-policy"></a>建立 off-by-default 原則  
  
1.  在物件總管中，以滑鼠右鍵按一下 [介面區組態]，然後按一下 [新增原則]。  
  
2.  在 [建立新原則] 對話方塊的 [名稱] 方塊中，輸入 **Off By Default**。 
    1. 將 [已啟用] 核取方塊保持不核取狀態。 [已啟用] 核取方塊會套用至自動原則，而且這個原則會視需要執行。
    1. 在 [檢查條件] 核取方塊中，向下捲動至 [介面區組態] 區域，然後選取 [Mail Off] 當作要檢查的條件。
    1. [針對目標] 方塊將呈現空白，因為這是伺服器範圍的原則。 
    1. 在 [評估模式] 核取方塊中，選取 [視需要] 當作評估模式。
    1. 在 [伺服器限制] 核取方塊中，選取 [無]。
    1. 在 [描述] 頁面上，輸入原則的描述。  

    ![off by default 原則](Media/lesson-1-create-and-apply-an-off-by-default-policy/off-by-default-policy.png)
  
9. 在描述頁面上，您可以在 [其他說明超連結] 區域中，為原則提供網頁的超連結。 在 [要顯示的文字] 方塊中，輸入要針對超連結顯示的文字。
    1. 在 [位址] 方塊中，輸入說明頁面的超連結，例如公司 IT 部門的首頁。
    1. 若要透過開啟網頁確認位址，請按一下 [測試連結]。
    1. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

    ![Off-by-default 原則 Web 連結](Media/lesson-1-create-and-apply-an-off-by-default-policy/off-by-default-policy-web-link.png)


## <a name="configure-server-to-run-off-by-default-policy"></a>設定伺服器以執行 off-by-default 原則 

1.  在物件總管中，以滑鼠右鍵按一下 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，指向 [原則]，然後按一下 [評估]。  

    ![評估原則](Media/lesson-1-create-and-apply-an-off-by-default-policy/evaluate-policy.png)
  
2.  在 [評估原則] 對話方塊中，您可以從另一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體或檔案中選取原則。 在這個步驟中，請將 [來源] 保持設定為 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體。  
    1. 在 [原則] 區段中，選取 [預設關閉] 原則。
    1. 若要查看伺服器是否符合此原則，請按一下 [評估]。
    1. 如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 符合此原則，您將會在 [結果] 區域中看見含有核取記號的綠色圓圈。 如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 不符合此原則，您就會看見含有 X 的紅色圓圈。 

   ![評估 off-by-default 原則](Media/lesson-1-create-and-apply-an-off-by-default-policy/evaluate-off-by-default-policy.png)

  
6.  在 [目標詳細資料] 區域中，您將會在錯誤發生時於 [訊息] 資料行中看到其他資訊。 在 [訊息] 資料行中，按一下 [檢視] 查看報表，其中包含所檢查之每個 Facet 屬性的檢查結果。 

    ![檢視原則評估的結果 ](Media/lesson-1-create-and-apply-an-off-by-default-policy/view-results-of-policy-evaluation.png)
  
7.  原則描述會顯示在頁面底部，而且 [其他說明] 區段會顯示您已針對此原則設定的超連結。 按一下訊息超連結，即可開啟您在建立此原則時指定的網頁。   

1.  關閉瀏覽器，然後關閉 [結果詳細檢視] 對話方塊。  

1. 如果伺服器不符合原則，而且您想要停用 Database Mail，請按一下 [評估結果] 頁面中的 [套用]。  
  
10. 關閉 [結果詳細檢視] 和 [評估原則] 對話方塊。   

   
## <a name="next-lesson"></a>下一課  
[第 2 課：建立和套用命名標準原則](../../relational-databases/policy-based-management/lesson-2-create-and-apply-a-naming-standards-policy.md)  
  
  
  
