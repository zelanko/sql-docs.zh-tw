---
title: "解除封裝 DAC 封裝 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-data-tier-apps"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "精靈 [DAC], 解除封裝"
  - "資料層應用程式 [SQL Server], 解除封裝"
  - "如何 [DAC], 解除封裝"
  - "解除封裝 DAC"
ms.assetid: 697b69b3-f157-4e22-ac4e-f65c5fc2d0ad
caps.latest.revision: 11
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 11
---
# 解除封裝 DAC 封裝
  使用 [解除封裝資料層應用程式] 對話方塊可從資料層應用程式 (DAC) 封裝解壓縮指令碼和檔案。 這些指令碼和檔案會放置在某個資料夾中，使用此封裝來將 DAC 部署到實際執行系統之前便可以進行檢閱。 DAC 的內容也可以與解除封裝到另一個資料夾的另一個封裝內容相比較。  
  
1.  **開始之前**  [安全性](#Security)  
  
2.  **使用下列項目，解除封裝 DAC：**[解除封裝資料層應用程式對話方塊](#UnpackDACDial)、[檢查 DAC 封裝的內容](#ExamDACPack)  
  
##  <a name="Security"></a> 安全性  
 建議您不要部署來源不明或來源不受信任的 DAC 封裝。 這類 DAC 可能包含惡意程式碼，因此可能會執行非預期的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼，或是修改結構描述而造成錯誤。 在您使用來源不明或來源不受信任的 DAC 之前，請將它部署到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的隔離測試執行個體、解除封裝 DAC 並檢查程式碼，例如預存程序或其他使用者定義的程式碼。  
  
##  <a name="UnpackDACDial"></a> 解除封裝資料層應用程式對話方塊  
 **解除封裝 DAC 封裝檔案**  
  
-   在 Windows 檔案總管中，巡覽至 DAC 封裝 (.dacpac) 檔案的位置。  
  
-   使用這兩種方法的其中一種，來開啟 [解除封裝資料層應用程式] 對話方塊：  
  
    1.  以滑鼠右鍵按一下 DAC 封裝 (.dacpac) 檔案，並選取 [解除封裝]。  
  
    2.  按兩下 DAC 封裝檔案。  
  
-   完成對話方塊：  
  
    -   [解除封裝 Microsoft SQL Server DAC 封裝檔案](#Unpack)  
  
    -   [瀏覽資料夾](#Browse)  
  
###  <a name="Unpack"></a> 解除封裝 Microsoft SQL Server DAC 封裝檔案  
 使用此頁面可指定要放置解除封裝檔案的目的地資料夾，然後執行解除封裝作業。  
  
 **檔案將解除封裝至這個資料夾** - 指定放置解除封裝檔案之資料夾的完整路徑。 如果此資料夾已經存在，而且您知道完整路徑，請在方塊中輸入路徑。 如果不存在，請按一下 **[瀏覽]** 按鈕，導覽至資料夾或建立新的資料夾。  
  
 **瀏覽** - 開啟 [瀏覽資料夾] 頁面，您可以在這裡導覽檔案階層來選擇資料夾或建立新的資料夾。  
  
 **解除封裝** - 開始解除封裝作業。  
  
 **取消** - 結束此對話方塊，而不解除封裝 DAC 封裝。  
  
###  <a name="Browse"></a> 瀏覽資料夾  
 使用此頁面可選擇解除封裝作業的目的地資料夾。 您也可以選擇建立新的資料夾。  
  
 **資料夾清單** - 顯示電腦的檔案階層。 展開節點，導覽至要解除封裝 DAC 封裝的資料夾。 按一下此資料夾，然後按一下 **[確定]**。  
  
 **建立新資料夾** - 開啟對話方塊，您可以在其中指定您目前在資料夾階層中選取之資料夾內所要建立的新資料夾名稱。  
  
 **確定** - 放置您在 [解除封裝 DAC 封裝檔案] 頁面之 [檔案將解除封裝至這個資料夾] 方塊內所選取之資料夾的路徑，並讓您回到這個頁面。  
  
 **取消** - 結束此對話方塊，而不選取資料夾。  
  
##  <a name="ExamDACPack"></a> 檢查 DAC 封裝的內容  
 在解除封裝之後，您可以檢查 [解除封裝資料層應用程式] 對話方塊所產生的檔案。 此對話方塊會在選取的目的地資料夾中建置下列檔案：  
  
1.  Transact-SQL 指令碼，其中包含建立 DAC 中所定義之物件的陳述式。 檔案名稱為 *DACName*.sql，其中 *DACName* 是 DAC 的名稱。  
  
2.  封裝中的所有 XML 檔案。  
  
3.  DAC [其他檔案] 區段中的所有檔案，例如 DAC 預先部署或部署後的檔案。  
  
 如需詳細資訊，請參閱 [Validate a DAC Package](../../relational-databases/data-tier-applications/validate-a-dac-package.md)。  
  
## 另請參閱  
 [資料層應用程式](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [部署資料層應用程式](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)   
 [升級資料層應用程式](../../relational-databases/data-tier-applications/upgrade-a-data-tier-application.md)  
  
  