---
title: "將知識庫匯出到 .dqs 檔案 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a324ead5-c8aa-4e26-abe3-ef415add00f8
caps.latest.revision: 19
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 19
---
# 將知識庫匯出到 .dqs 檔案
  此主題描述如何將整個知識庫匯出到 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中的 .dqs 資料檔。 您可以將定義域或整個知識庫匯出到資料檔。 匯出網域的相關資訊，請參閱 [將定義域匯出成.dqs 檔案](../data-quality-services/export-a-domain-to-a-dqs-file.md)。  
  
 將知識庫匯出到 .dqs 檔，然後將此檔案當做另一個知識庫匯入將會簡化知識產生程序，以節省時間與精力。 這樣可讓您將知識庫和其知識與其他人分享。 .dqs 檔將包含所有知識庫資訊，包括定義域和比對原則，但不包括附加的參考資料資訊。 匯入 .dqs 檔之後，如有必要，您必須將必要的定義域再次附加至適當的參考資料服務。 知識庫中已發行和未發行的資料都會匯出。  
  
 匯出程序所建立的 .dqs 資料檔已經過加密，因此無法檢視內容。  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 必要條件  
 若要將知識庫匯出到 .dqs 資料檔，您必須已建立及開啟知識庫。 您不需要擁有匯出目標的 .dqs 檔案，系統會為您建立一個檔案。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 您必須擁有 DQS_MAIN 資料庫的 dqs_kb_editor 角色或 dqs_administrator 角色，才能將知識庫匯出到 .dqs 資料檔。  
  
##  <a name="Export"></a> 將知識庫匯出到 .dqs 檔案  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [執行資料品質用戶端應用程式](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面中，於 [定義域管理] 活動中開啟知識庫。  
  
3.  在定義域管理頁面 （包含任何選取的索引標籤） 中，按一下 [ **匯出知識庫資料** 網域清單，然後按一下上方圖示 **匯出知識庫**。 或者，您可以也以滑鼠右鍵按一下 **網域** 清單中，將滑鼠停留在 **匯出**, ，然後按一下 [ **匯出知識庫**。  
  
4.  在 **匯出到資料檔** ] 對話方塊中，移至您想要儲存檔案名稱中的檔案或是保留知識庫名稱、 資料夾保留 **DQS 資料檔 (\*.dqs)** 為 **存** 輸入，然後再按一下 **儲存**。  
  
5.  在 **[匯出知識庫]** 對話方塊中，確認狀態行指出已完成匯出。 按一下 **[確定]**。  
  
##  <a name="FollowUp"></a> 後續操作：將定義域匯出到 .dqs 檔案之後  
 當您將知識庫匯出到 .dqs 檔案之後，您可以將此知識庫匯入相同的 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] (具有新的名稱) 或不同的 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]。  
  
  