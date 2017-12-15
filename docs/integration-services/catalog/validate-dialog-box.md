---
title: "驗證對話方塊 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: service
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ssis.ssms.isprojectvalidate.f1
- sql13.ssis.ssms.ispackagevalidate.f1
ms.assetid: 134e14ce-4f8d-4a20-889a-918014c841d8
caps.latest.revision: "7"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1074a29bfb5b8a8c05114f08b5160223b5bbdd6e
ms.sourcegitcommit: 6bbecec786b0900db86203a04afef490c8d7bfab
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/12/2017
---
# <a name="validate-dialog-box"></a>驗證對話方塊
  使用 **[驗證]** 對話方塊檢查 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案或封裝中的常見問題。  
  
 如果有問題，就會在對話方塊上方顯示一個訊息。 否則，「就緒」這個詞會顯示在上方。  
  
 **您想要做什麼事？**  
  
-   [開啟 [驗證] 對話方塊](#open_dialog)  
  
-   [設定 [一般] 頁面上的選項](#general)  
  
##  <a name="open_dialog"></a> 開啟 [驗證] 對話方塊  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，連接至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器。  
  
     您正在連接到主控 SSISDB 資料庫之 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體。  
  
2.  在 [物件總管] 中，展開樹狀目錄以顯示 **[Integration Services 目錄]** 節點。  
  
3.  展開 **[SSISDB]** 節點。  
  
4.  展開包含您要驗證之專案或封裝的資料夾。  
  
5.  以滑鼠右鍵按一下封裝，然後按一下 [驗證]。  
  
##  <a name="general"></a> 設定 [一般] 頁面上的選項  
 **環境**  
 選取您要用來驗證專案或封裝的環境。  
  
 **32 位元執行階段**  
 選擇使用 32 位元執行階段執行封裝。  
  
 **[參數]** 索引標籤會列出您用來驗證專案或封裝的參數值。 以下是在 [參數] 索引標籤上的選項。  
  
 **容器**  
 列出包含參數的物件。  
  
 **參數**  
 列出參數的名稱  
  
 **Value**  
 列出參數值。  
  
 **[連接管理員]** 索引標籤會列出您用來驗證專案或封裝的連接管理員屬性值。  
  
 以下是在 **[連接管理員]** 索引標籤上的選項。  
  
 **容器**  
 列出包含連接管理員的物件。  
  
 **名稱**  
 列出連接管理員名稱。  
  
 **屬性名稱**  
 列出連接管理員屬性的名稱。  
  
 **Value**  
 列出指派給連接管理員屬性的值。  
  
  
