---
title: "管理知識庫 | Microsoft Docs"
ms.custom: ""
ms.date: "06/04/2013"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 27f306f4-d67c-47f5-b35c-4260cc5d36e3
caps.latest.revision: 9
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 9
---
# 管理知識庫
  本主題描述如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中針對知識庫執行管理功能。 您可以刪除知識庫、解除鎖定知識庫、捨棄知識庫工作、重新命名知識庫，以及顯示其屬性。  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 必要條件  
 若要管理知識庫，該知識庫必須已經建立完成，而且它必須已發行 (如果是由另一個人建立) 或關閉 (如果是由您建立)。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 您必須擁有 DQS_MAIN 資料庫的 dqs_kb_editor 角色或 dqs_administrator 角色，才能開啟知識庫。  
  
##  <a name="Manage"></a> 管理知識庫  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [執行資料品質用戶端應用程式](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面上，按一下 **[開啟知識庫]**。  
  
3.  以滑鼠右鍵按一下知識庫資料表中的知識庫。  
  
4.  在內容功能表中，您可以進行下列作業：  
  
    1.  **開啟**︰ 按一下以開啟 「 知識庫 」 中所選活動 **選取活動** 窗格。  
  
    2.  **解除鎖定**︰ 如果您正在處理知識庫中的其中一個步驟定義域管理、 知識探索和比對原則活動，而且已關閉的使用者，您可以解除鎖定知識庫。 如果您解除鎖定知識庫，另一位人員就能夠開啟並處理知識庫。 如果知識庫並未處於活動的狀態，您就無法使用此命令。 如需詳細資訊，請參閱 [開啟知識庫](../data-quality-services/open-a-knowledge-base.md)。  
  
    3.  **捨棄工作**︰ 時，按一下知識庫處於正在處理，如資料表中的 [狀態] 欄位中的項目所示。 如果知識庫並未處於活動的狀態，您就無法使用此命令。如果知識庫已鎖定，您也無法使用此命令。 如需詳細資訊，請參閱 [開啟知識庫](../data-quality-services/open-a-knowledge-base.md)。  
  
    4.  **重新命名**︰ 按一下即可讓知識庫資料表的欄位上以滑鼠右鍵按一下的知識庫可編輯。 請變更名稱，然後按一下該知識庫和欄位中的另一個知識庫，接受名稱變更。  
  
    5.  **刪除**: DQS_MAIN 資料庫中移除知識庫上按一下 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]。  
  
    6.  **屬性**︰ 按一下以顯示在唯讀模式顯示資料庫的屬性。  
  
        1.  **來源知識庫**︰ 此資料庫為基礎的知識庫。 這是選擇性的。  
  
        2.  **狀態**︰ 指出知識庫是否 **工作中** ，而且如果是在特定的知識管理活動中，決定上次關閉。 此狀態可能是 **工作中**, 中的 「 知識庫 」 開啟在知識管理工作階段，而不是特定活動，或 **工作中** 再加上知識管理活動，在知識管理工作階段，並進行特定活動，開啟知識庫。  
  
        3.  **已鎖定**: **True** 如果知識庫已鎖定， **False** 如果不是  
  
        4.  **包含未發行的內容**︰ 如果知識庫包含尚未儲存的發行，否則為 False 不的內容則為 True  
  
        5.  **鎖定者**︰ 關閉知識庫並加以鎖定之使用者的名稱  
  
        6.  **鎖定日期**︰ 鎖定的日期  
  
        7.  **建立者**︰ 建立知識庫，他或她所屬的網路的使用者名稱  
  
        8.  **建立日期**︰ 建立的日期  
  
##  <a name="FollowUp"></a> 後續操作：管理知識庫之後  
 管理知識庫之後，下一個步驟將取決於您針對知識庫所採取的動作：  
  
-   如果您開啟了知識庫，就要繼續進行已選取的活動。  
  
-   如果您解除鎖定了知識庫，另一位人員就可以在指出的狀態中開啟並處理該知識庫。  
  
-   如果您捨棄了知識庫工作，該知識庫將處於上次發行的狀態。  
  
-   如果您重新命名了知識庫，就必須開啟已重新命名的知識庫，才能進行處理。  
  
-   如果您刪除了知識庫，就必須選取另一個要處理的知識庫，或是建立新的知識庫。  
  
  