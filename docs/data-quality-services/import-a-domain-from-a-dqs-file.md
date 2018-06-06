---
title: 從 .dqs 檔案匯入定義域 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.component: data-quality-services
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: fabd88b0-22b3-4543-a993-6d5b202ded80
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 37ad741fa01ebc8af4f123beef73aa66c9793fbe
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="import-a-domain-from-a-dqs-file"></a>從 .dqs 檔案匯入定義域

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  此主題描述如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中將 .dqs 檔案中的定義域匯入現有的知識庫中。 .dqs 資料檔的建立方式是從 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 應用程式匯出定義域或知識庫。 .dqs 資料檔已加密，所以無法檢視。  
  
 使用 .dqs 資料檔匯出某個知識庫中的定義域，然後將它匯入另一個知識庫將會簡化知識產生程序，以節省時間與精力。 這樣可讓您將定義域和定義域的知識與其他人分享，以節省他們的時間。 您可以匯入一個單一定義域或一個複合定義域 (包含多個單一定義域)。 包含單一定義域的 .dqs 檔案包括所有定義域資料，其中包括定義域屬性、值和規則資料，但不包括對應的參考資料資訊。 含有複合定義域的 .dqs 檔案包括所有複合定義域資料，其中包括複合定義域內所容納之單一定義域的所有定義域資料，以及複合定義域屬性、值關聯和 CD 規則，但不包括對應的參考資料。 已發行和未發行的資料都將匯入。  
  
 當您匯入定義域時，此定義域的名稱依然與一開始匯出的定義域名稱相同，除非此定義域名稱已經存在 (此時 DQS 會在名稱中附加 “_1”)。 如果您匯入的複合定義域所包含的個別定義域與現有定義域同名，這個情況也會成立。  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 必要條件  
 若要從 .dqs 檔案匯入定義域，您必須已將一個單一定義域或是一個複合定義域 (包含多個單一定義域) 匯出到 .dqs 檔案。 此 .dqs 檔案只能包含一個定義域。 您也必須已建立及開啟知識庫，才能將定義域匯入其中。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 您必須擁有 DQS_MAIN 資料庫的 dqs_kb_editor 角色或 dqs_administrator 角色，才能從 .dqs 資料檔匯入定義域。  
  
##  <a name="Import"></a> Import a domain from a .dqs file  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [執行 Data Quality Client 應用程式](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面中，於 [定義域管理] 活動中開啟知識庫。  
  
3.  按一下 **[從資料檔匯入定義域]** 圖示。  
  
4.  在 **[從資料檔匯入]** 對話方塊中，移至包含您要匯入之檔案的資料夾，然後選取檔案 (檔案類型為 DQS 檔案)，再按一下 **[開啟]**。  
  
5.  在 **[匯入定義域]** 對話方塊中，按一下 **[確定]**。  
  
    > [!NOTE]  
    >  只有當匯入的來源 .dqs 檔案只包含一個單一定義域或是一個複合定義域 (包含多個單一定義域) 時，匯入作業才會成功。  
  
6.  確認您匯入的定義域顯示在 **[定義域]** 清單中。 如果您匯入複合定義域，請確認此複合定義域以及其中包含的單一定義域全都位於 **[定義域]** 清單中。  
  
##  <a name="FollowUp"></a> 後續操作：從 .dqs 檔案匯入定義域之後  
 當您從 .dqs 檔案匯入定義域之後，您可以將知識加入至定義域，或是在清理或比對專案中使用定義域 (根據定義域的內容而定)。 如需詳細資訊，請參閱[執行知識探索](../data-quality-services/perform-knowledge-discovery.md)、[管理定義域](../data-quality-services/managing-a-domain.md)、[管理複合定義域](../data-quality-services/managing-a-composite-domain.md)、[建立比對原則](../data-quality-services/create-a-matching-policy.md)、[資料清理](../data-quality-services/data-cleansing.md)或[資料比對](../data-quality-services/data-matching.md)。  
  
  
