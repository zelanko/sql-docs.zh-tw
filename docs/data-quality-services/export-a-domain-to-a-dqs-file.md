---
title: "將定義域匯出成 .dqs 檔案 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: eba10d3d-b5c4-447b-8a30-fa07996cb28e
caps.latest.revision: 18
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 18
---
# 將定義域匯出成 .dqs 檔案
  此主題描述如何在 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中將定義域匯出至 .dqs 檔案。 您可以將定義域或整個知識庫匯出到資料檔。 匯出知識庫的相關資訊，請參閱 [將知識庫匯出到.dqs 檔案](../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)。  
  
 將某個知識庫中的定義域匯出到 .dqs 資料檔，然後將它匯入另一個知識庫將會簡化知識產生程序，以節省時間與精力。 這樣可讓您將定義域和定義域的知識與其他人分享。  
  
 您可以匯出單一定義域或複合定義域。 包含單一定義域的 .dqs 檔案包括所有定義域資料，其中包括定義域屬性、值和規則，但不包括附加的參考資料資訊。 含有複合定義域的 .dqs 檔案包括所有複合定義域資料，其中包括複合定義域內所容納之定義域的所有定義域資料，以及複合定義域屬性、關聯和規則，但不包括參考資料資訊。 匯入 .dqs 檔之後，如有必要，您必須將定義域或複合定義域再次附加至適當的參考資料服務。 已發行和未發行的資料都會匯出。  
  
 匯出程序所建立的 .dqs 資料檔已經過加密，因此無法檢視內容。  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 必要條件  
 若要將定義域匯出到 .dqs 資料檔，您必須已經建立及選取單一定義域或是包含多個單一定義域的複合定義域。 您不需要擁有匯出目標的 .dqs 檔案，系統會為您建立一個檔案。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 您必須擁有 DQS_MAIN 資料庫的 dqs_kb_editor 角色或 dqs_administrator 角色，才能將定義域匯出到 .dqs 資料檔。  
  
##  <a name="Export"></a> 將定義域匯出成 .dqs 檔案  
 您可以從任何 [定義域管理] 頁面匯出。 您可以從使用者介面的控制項或是 [定義域清單] 窗格之內容功能表的命令中取得匯出命令。  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [執行資料品質用戶端應用程式](../data-quality-services/run-the-data-quality-client-application.md)。  
  
2.  在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 首頁畫面中，於 [定義域管理] 活動中開啟知識庫。  
  
3.  在 **網域管理頁面** （包含任何索引標籤選取），選取單一定義域或複合定義域中的 **網域** 清單。  
  
4.  按一下定義域清單上方的 **[匯出知識庫資料]** 圖示，然後按一下 **[匯出定義域]**。 或者，您可以以滑鼠右鍵按一下網域中的 **網域** 清單中，指向 [ **匯出**, ，然後按一下 [ **匯出定義域**。  
  
5.  在 **匯出到資料檔** ] 對話方塊中，移至您想要儲存檔案名稱中的檔案，或保留預設名稱，資料夾保留 **DQS 資料檔 (\*.dqs)** 為 **檔案類型**, ，然後按一下 [ **儲存**。  
  
6.  在 **[匯出定義域]** 對話方塊中，確認此對話方塊中的狀態行指出已完成匯出。 按一下 **[確定]**。  
  
##  <a name="FollowUp"></a> 後續操作：將定義域匯出到 .dqs 檔案之後  
 在您將定義域匯出到 .dqs 檔案之後，您可以將此定義域匯入另一個知識庫中。  
  
  