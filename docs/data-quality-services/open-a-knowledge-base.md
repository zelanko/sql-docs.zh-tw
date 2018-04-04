---
title: 開啟知識庫 | Microsoft Docs
ms.custom: ''
ms.date: 06/04/2013
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: ''
ms.component: data-quality-services
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dqs.kb.openkb.f1
ms.assetid: a5f010a5-b762-41c9-881b-bf0c192dca83
caps.latest.revision: ''
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4cf7aa8e7fe21b83ee28a2bf2212823897fef9eb
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2018
---
# <a name="open-a-knowledge-base"></a>開啟知識庫
  此主題描述如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中開啟現有的知識庫，並預備此知識庫進行定義域管理、知識探索或是加入比對原則。  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 必要條件  
 若要開啟知識庫，必須已建立該知識庫，而且它必須已發行 (如果是由另一個人建立) 或關閉 (如果是由您建立)。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 您必須擁有 DQS_MAIN 資料庫的 dqs_kb_editor 角色或 dqs_administrator 角色，才能開啟知識庫。  
  
##  <a name="Open"></a> Open a knowledge base  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [執行 Data Quality Client 應用程式](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面上，按一下 **[開啟知識庫]**。  
  
3.  在資料表中選取知識庫。 知識庫中的定義域和比對規則將會顯示在頁面的右窗格中。  
  
    > [!NOTE]  
    >  您可以在資料表中按一下滑鼠右鍵，對知識庫執行作業。 您可以開啟知識庫、以另一個名稱儲存、解除鎖定、捨棄工作、重新命名或顯示其屬性。  
  
4.  在 **[選取活動]**中，選取您想要在知識庫上執行的活動：  
  
    -   選取 **[定義域管理]** ，進入用來修改知識庫內之定義域的畫面。  
  
    -   選取 **[知識探索]** ，進入用來分析資料樣本並以結果擴展知識庫定義域的精靈。  
  
    -   選取 **[比對原則]** 建立比對原則，並將其加入至知識庫。  
  
5.  按一下 **[開啟]**。  
  
    > [!NOTE]  
    >  若要開啟知識庫，您也可以在知識庫上按一下滑鼠右鍵，然後按一下 [開啟]。 內容功能表中的其他命令可讓您以另一個名稱儲存、解除鎖定、捨棄工作、重新命名或顯示其屬性。  
  
    > [!NOTE]  
    >  如果您因為知識庫已鎖定所以無法將它開啟，請參閱底下的章節。  
  
## <a name="open-a-recent-knowledge-base"></a>開啟最近使用的知識庫  
 最近開啟的五個知識庫會顯示在 DQS 首頁的 **[最近使用的知識庫]** 清單中。 如此可讓您開啟最近使用過的知識庫，而不需要透過 **[開啟知識庫]** 頁面。  
  
-   若要在最近使用清單中開啟未鎖定的知識庫，請按一下知識庫的向右箭號，然後選取您要開啟之知識庫所在的活動。  
  
-   若要在最近使用清單中開啟您鎖定的知識庫，請按一下知識庫，它就會在括號所指示的活動與頁面中開啟。  
  
-   若要在最近使用清單中開啟已由他人鎖定的知識庫，請連絡這個人，請他解除鎖定知識庫。  
  
##  <a name="FollowUp"></a> 後續操作：開啟知識庫之後  
 在您開啟知識庫之後，此知識庫會處於 [知識庫] 資料表的 [狀態] 資料行所指示的狀態。 如果是知識探索和比對原則活動，將會在特定精靈頁面中開啟知識庫。 如果是定義域管理活動，將會在定義域管理頁面中開啟知識庫。 如需狀態的詳細資訊，請參閱[執行知識探索](../data-quality-services/perform-knowledge-discovery.md)、[管理定義域](../data-quality-services/managing-a-domain.md)或[建立比對原則](../data-quality-services/create-a-matching-policy.md)。  
  
##  <a name="Locked"></a> 如果知識庫已鎖定  
 第一個資料行中的鎖定圖示顯示知識庫是否已鎖定。 已鎖定的知識庫名稱將會是紅色字型。 特定使用者透過知識庫活動正在修改的知識庫會標示為已鎖定。 鎖定的知識庫無法由另一個使用者操作。 正在處理知識庫的使用者若要將知識庫解除鎖定，可以在 [開啟知識庫] 頁面上資料表中的知識庫上按一下滑鼠右鍵，然後按一下 **[解除鎖定]**，或是發行知識庫。 當游標置於鎖定的知識庫上時，DQS 將會顯示一個提示，指示鎖定知識庫的人以及鎖定的時間。  
  
##  <a name="State"></a> 知識庫的狀態  
 狀態欄位會指示知識庫位於活動的哪一個階段。 如果您開啟知識庫，它將會開啟到這個階段。  
  
-   **\<空白>**：知識庫的 [狀態] 欄位空白的條件如下：已在 [定義域管理] 活動中按一下 [發行]，然後按一下 [是 - 發行知識庫並結束] 來發行知識庫。  
  
-   **工作中**：已在 [定義域管理] 活動中按一下 **[發行]** ，然後按一下 **[否 - 儲存知識庫工作並結束]**來儲存知識庫工作。  
  
-   **定義域管理**：已輸入知識庫的定義域資料，但尚未發行知識庫，而且工作仍在 [定義域管理] 活動中。 知識探索活動無法使用。 當您在 **[定義域管理]** 畫面中按一下 **[關閉]** 時，就會發生這種狀況。  
  
-   **探索 - 對應**：已在 **[知識庫管理: 對應]** 頁面上關閉知識庫。 知識庫已鎖定，無法使用 [定義域管理] 和 [比對] 活動。  
  
-   **探索 - 探索**：已在 **[知識庫管理: 分析]** 頁面上關閉知識庫。 知識庫已鎖定，[定義域管理] 活動無法使用。  
  
-   **探索 - 值管理**：已在 **[知識庫管理: 管理定義域詞彙]** 頁面上關閉知識庫。 知識庫已鎖定，[定義域管理] 活動無法使用。  
  
-   **比對原則 – 比對原則**：已在 **[比對原則 – 比對原則]** 頁面上關閉知識庫。 知識庫已鎖定，無法使用 [知識探索] 和 [定義域管理] 活動。  
  
-   **比對原則 – 比對結果**：已在 **[比對原則 – 比對結果]** 頁面上關閉知識庫。 知識庫已鎖定，無法使用 [知識探索] 和 [定義域管理] 活動。  
  
  
