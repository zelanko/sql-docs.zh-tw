---
title: "建立和對應伺服器環境 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.ssms.isenvprop.permissions.f1"
  - "sql13.ssis.ssms.isenvprop.general.f1"
  - "sql13.ssis.ssms.iscreateenv.f1"
  - "sql13.ssis.ssms.isenvprop.variables.f1"
ms.assetid: b1cbb697-713f-48e4-b234-b23724d87451
caps.latest.revision: 12
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 12
---
# 建立和對應伺服器環境
  您可以建立伺服器環境，針對已部署至 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 伺服器之專案中所包含的封裝，指定執行值。 接著您可以針對特定封裝、進入點封裝，或給定專案中的所有封裝，將環境變數對應至參數。 進入點封裝通常是執行子封裝的父封裝。  
  
> [!IMPORTANT]  
>  對於某個特定執行，封裝只能藉由單一伺服器環境中包含的值執行。  
  
 您可以透過查詢檢視表，取得伺服器環境、環境參考和環境變數的清單。 您也可以呼叫預存程序來加入、刪除及修改環境、環境參考和環境變數。 如需詳細資訊，請參閱 [SSIS 目錄](../../integration-services/service/ssis-catalog.md)中的＜伺服器環境、伺服器變數和伺服器環境參考＞一節。  
  
### 若要建立和使用伺服器環境  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 的物件總管中，展開 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 目錄> **SSISDB** 節點，然後針對您要建立其環境的專案，尋找 [環境] 資料夾。  
  
2.  在以滑鼠右鍵按一下 [環境] 資料夾，然後按一下 [建立環境]。  
  
3.  輸入環境的名稱，並選擇性地輸入描述，然後按一下 [確定]。  
  
4.  以滑鼠右鍵按一下新環境，然後按一下 [屬性]。  
  
5.  在 [變數] 頁面上執行下列動作，以加入變數。  
  
    1.  選取變數的 [類型]。 變數的名稱**無須**與對應至該變數之專案參數的名稱相符。  
  
    2.  選擇性地輸入變數的 [描述]。  
  
    3.  輸入環境變數的 [值]。  
  
         如需環境變數名稱規則的資訊，請參閱 [SSIS 目錄](../../integration-services/service/ssis-catalog.md)中的＜環境變數＞一節。  
  
    4.  選取或清除 [區分] 核取方塊，以指出此變數是否包含機密值。  
  
         如果您選取 [區分]，變數值就不會顯示在 [值] 欄位內。  
  
         機密值將在 SSISDB 目錄中進行加密。 如需加密的詳細資訊，請參閱 [SSIS 目錄](../../integration-services/service/ssis-catalog.md)。  
  
6.  在 [權限] 頁面上執行下列動作，對選取的使用者和角色授與或拒絕任何權限。  
  
    1.  按一下 [瀏覽]，然後從 [瀏覽所有主體] 對話方塊中選取一個或多個使用者和角色。  
  
    2.  在 [登入或角色] 區域內，選取您想要授與或拒絕其權限的使用者或角色。  
  
    3.  在 [明確] 區域內，按一下每項權限旁的 [授與] 或 [拒絕]。  
  
7.  若要編寫環境的指令碼，請按一下 [指令碼]。 預設情況下，指令碼會顯示在新的 [查詢編輯器] 視窗中。  
  
    > [!TIP]  
    >  只要環境屬性有所增減或變更 (例如加入變數)，您就必須按一下 [指令碼]，然後才按一下 [環境屬性] 對話方塊中的 [確定]。 否則將不會產生指令碼。  
  
8.  按一下 [確定]，將變更儲存至環境屬性。  
  
9. 在物件總管中的 [SSISDB] 節點下，展開 [專案] 資料夾，以滑鼠右鍵按一下專案，然後按一下 [設定]。  
  
10. 在 [參考] 頁面上，按一下 [加入] 加入環境，然後按一下 [確定] 將參考儲存至環境。  
  
11. 再次以滑鼠右鍵按一下專案，然後按一下 [設定]。  
  
12. 若要將環境變數對應至您在設計階段加入封裝中的參數，或對應至您將 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案轉換為專案部署模型時所產生的參數，請執行下列操作。  
  
    1.  在 [參數] 頁面的 [參數] 索引標籤中，按一下 [值] 欄位旁的瀏覽按鈕。  
  
    2.  按一下 [使用環境變數]，然後選取您建立的環境變數。  
  
13. 若要將環境變數對應至連線管理員屬性，請執行下列操作。 SSIS 伺服器上會自動產生連接管理員屬性的參數。  
  
    1.  在 [參數] 頁面的 [連線管理員] 索引標籤中，按一下 [值] 欄位旁的瀏覽按鈕。  
  
    2.  按一下 [使用環境變數]，然後選取您建立的環境變數。  
  
14. 按兩次 [確定]，以儲存您的變更。  
  
  