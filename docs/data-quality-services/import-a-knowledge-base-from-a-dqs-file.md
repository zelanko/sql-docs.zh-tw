---
title: "從 .dqs 檔案匯入知識庫 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: 
ms.component: data-quality-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9b9786fe-9e80-429a-afcb-dc3b3dd6f0b0
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9914672b055d007c76e55f70a87c7af71225de0a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="import-a-knowledge-base-from-a-dqs-file"></a>從 .dqs 檔案匯入知識庫
  此主題描述如何從 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中的 .dqs 資料檔匯入整個知識庫。 您從 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 應用程式匯出現有的知識庫來建立此資料檔 (請參閱＜ [將知識庫匯出到.dqs 檔案](../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)＞)。  
  
 使用 .dqs 資料檔匯出知識庫的內容，然後將內容匯入相同 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 或不同 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 上的另一個知識庫會簡化知識產生程序，以節省時間與精力。 這樣可讓您將知識庫和知識庫的知識與其他人分享，以節省他們的時間。 .dqs 檔將包含所有知識庫資訊，包括定義域和比對原則，但不包括附加的參考資料資訊。 已發行和未發行的資料都將匯入。  
  
 .dqs 資料檔已加密，所以無法檢視。  
  
 當您匯入知識庫時，您可以使用相同的名稱，除非此知識庫名稱已存在於用戶端應用程式中 (此時必須重新命名)。  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 必要條件  
 若要從 .dqs 檔案匯入知識庫，您必須已將知識庫匯出到 .dqs 檔案。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 您必須擁有 DQS_MAIN 資料庫的 dqs_kb_editor 角色或 dqs_administrator 角色，才能從 .dqs 資料檔匯入知識庫。  
  
##  <a name="Import"></a> Import a knowledge base from a .dqs file  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [執行 Data Quality Client 應用程式](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面上，按一下 **[新增知識庫]**。  
  
3.  輸入知識庫的名稱。  
  
4.  按一下 **[建立知識庫來源]**的向下箭號，然後選取 **[從 DQS 檔案匯入]**。  
  
5.  針對 **[選取資料檔]**按一下 **[瀏覽]**。  
  
6.  在 **[從資料檔匯入]** 對話方塊中，移至包含您要匯入之 .dqs 檔案的資料夾，然後按一下檔案的名稱。 按一下 **[開啟]**。  
  
7.  確認 **[定義域]** 清單中是否顯示正確的知識庫和定義域。  
  
8.  請選取您要執行的活動，然後按一下 **[建立]**。  
  
9. 在 **[匯入知識庫]** 對話方塊中，確認狀態行指出已完成匯入。 按一下 **[確定]**。  
  
10. 完成您需要執行的知識探索、定義域管理或比對原則工作，然後按一下 **[完成]**。  
  
11. 按一下 **[發行]** 發行知識庫中的知識，或是按一下 **[否]** ，不發行。  
  
12. 如果您已發行知識庫，請按一下 **[確定]**。  
  
13. 在 Data Quality Services 首頁上，確認此知識庫列在 **[最近使用的知識庫]**底下。  
  
##  <a name="FollowUp"></a> 後續操作：從 .dqs 檔案匯入知識庫之後  
 當您從 .dqs 檔案匯入知識庫之後，您可以將知識加入至知識庫，或是在清理或比對專案中使用此知識庫 (根據知識庫的內容而定)。 如需詳細資訊，請參閱[執行知識探索](../data-quality-services/perform-knowledge-discovery.md)、[管理定義域](../data-quality-services/managing-a-domain.md)、[管理複合定義域](../data-quality-services/managing-a-composite-domain.md)、[建立比對原則](../data-quality-services/create-a-matching-policy.md)、[資料清理](../data-quality-services/data-cleansing.md)或[資料比對](../data-quality-services/data-matching.md)。  
  
  

