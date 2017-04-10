---
title: "儲存 SSIS 封裝 (SQL Server 匯入和匯出精靈) | Microsoft Docs"
ms.custom: ""
ms.date: "02/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.impexpwizard.savedtspackage.f1"
ms.assetid: 7bf8ac6a-5599-43ab-bf5c-e072c11b85a0
caps.latest.revision: 64
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 61
---
# 儲存 SSIS 封裝 (SQL Server 匯入和匯出精靈)
  如果您在 [儲存並執行封裝] 頁面指定要儲存精靈建立的 SSIS 封裝，[[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈] 會顯示 [儲存 SSIS 封裝]。 在此頁面上，您可以指定儲存封裝的其他選項  

您之前在 [儲存並執行封裝] 頁面上為將封裝儲存到 SQL Server 或檔案系統所執行的選擇，決定您在 [儲存 SSIS 封裝] 頁面中看到的選項。 若要再次查看 [儲存並執行封裝] 頁面，請參閱[儲存並執行封裝](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)。
 
**什麼是套件？** 精靈使用 SQL Server Integration Services (SSIS) 複製資料。 在 SSIS 中，基本的單位就是封裝。 當您在精靈的頁面間移動並指定選項時，精靈會在記憶體中建立 SSIS 封裝。
 
## <a name="screen-shot---save-the-package-in-the-file-system"></a>螢幕擷取畫面 - 將套件儲存在檔案系統
 
以下顯示的螢幕擷取畫面，是您在 [儲存並執行封裝] 頁面選取 [檔案系統] 選項後，精靈的 [儲存 SSIS 封裝] 頁面。 
  
![Save SSIS Package page of the Import and Export Wizard](../../integration-services/import-export-data/media/save-package1.png "Save SSIS Package page of the Import and Export Wizard")  

## <a name="screen-shot---save-the-package-in-sql-server"></a>螢幕擷取畫面 - 將套件儲存在 SQL Server

 以下顯示的螢幕擷取畫面，是您在 [儲存並執行封裝] 頁面選取 [SQL Server] 選項後，精靈的 [儲存 SSIS 封裝] 頁面。 
  
![Save SSIS Package page of the Import and Export Wizard](../../integration-services/import-export-data/media/save-package2.png "Save SSIS Package page of the Import and Export Wizard")  
  
## <a name="provide-a-name-and-description-for-the-package"></a>提供套件的名稱和描述  
 **名稱**  
 提供封裝的唯一名稱。  
  
 **描述**  
 提供封裝的描述。 最佳作法是描述封裝用途，使封裝可以自我記錄並易於維護。  
  
 **目標**  
 您之前為套件指定的目的地 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或檔案系統)。 如果想將封裝儲存至不同的目的地，請返回 [儲存並執行封裝] 頁面。
  
## <a name="save-the-package-in-the-file-system"></a>將封裝儲存在檔案系統 
如已選取檔案系統目的地，請完成下列欄位。

 **檔案名稱**  
 輸入目的地檔案的路徑和檔名，或使用 [瀏覽] 按鈕選取目的地。  
  
> [!TIP] 請務必透過輸入或瀏覽方式指定目的地資料夾。 如果只輸入檔案名稱而不輸入路徑，您就不知道精靈儲存封裝的位置。 此外，精靈也可能會嘗試將封裝儲存在您無權儲存檔案的位置，進而引發錯誤。  
>   
>  請記住封裝檔案的儲存位置。  
  
 **瀏覽**  
 或者使用 [儲存封裝] 對話方塊，瀏覽以選取目的地檔案的路徑。  

## <a name="save-the-package-in-sql-server"></a>將封裝儲存在 SQL Server 
如已選取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目的地，請完成下列欄位。

精靈會將 **msdb** 資料庫的封裝儲存在 **sysssispackages** 資料表中。
 
 > [!NOTE] 這個選項不會將封裝儲存在 SSIS 目錄資料庫 (SSISDB) 中。  
 
 **伺服器名稱**  
 輸入或選取目的地伺服器名稱。  
   
 **使用 Windows 驗證**  
使用 Windows 整合式驗證連接到伺服器。 這是慣用的驗證方法。  
  
 **使用 SQL Server 驗證**  
使用 SQL Server 驗證連接到伺服器。  
  
 **使用者名稱**  
如已指定 SQL Server 驗證，請輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用者名稱。  
  
 **密碼**  
如已指定 SQL Server 驗證，請輸入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 密碼。  
  
## <a name="about-the-two-pages-of-options-for-saving-the-package"></a>有關儲存封裝選項的兩個頁面  
 [儲存 SSIS 封裝] 頁面是挑選用來儲存 SSIS 封裝選項的兩個頁面之一。  
  
-   在前一個 [Save and Execute Package (儲存並執行封裝)] 頁面中，您選擇將封裝儲存在 SQL Server 中或存為檔案。 您還可以為儲存的封裝選擇安全性設定。 若要再次查看 [儲存並執行封裝] 頁面，請參閱[儲存並執行封裝](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)。  
  
-   在目前的頁面上，您提供封裝名稱以及儲存的詳細資訊。  
 
## <a name="run-the-saved-package-again-later"></a>稍後再次執行已儲存的封裝  
 若要了解稍後如何再次執行已儲存的封裝，請參閱下列主題之一。  
  
-   若要以具有好用的使用者介面的公用程式來執行封裝，請參閱[執行封裝公用程式 &#40;DtExecUI&#41; UI 參考](../../integration-services/packages/execute-package-utility-dtexecui-ui-reference.md)。  
  
-   若要從命令列或批次檔執行封裝，請參閱 [dtexec 公用程式](../../integration-services/packages/dtexec-utility.md)。  
  
-   如果是在檔案系統中儲存封裝，請參閱[在 SQL Server Data Tools 中執行封裝](../../integration-services/packages/run-a-package-in-sql-server-data-tools.md)在開發環境中執行封裝。 您必須先將封裝加入 Integration Services 專案中，才能開啟並執行它。  
 
-   如果是在 SQL Server 的 **msdb** 資料庫中儲存封裝，請連接到 Integration Services 服務。 然後，在 SQL Server Management Studio 的物件總管中，巡覽至 [存放的封裝 |MSDB]，以滑鼠右鍵按一下封裝，然後選取 [執行封裝]。

## <a name="customize-the-saved-package"></a>自訂已儲存的封裝  
 若要了解如何自訂已儲存的封裝，請參閱 [Integration Services &#40;SSIS&#41; 封裝](../../integration-services/integration-services-ssis-packages.md)。  
  
## <a name="whats-next"></a>下一步  
 指定儲存封裝的其他選項之後，下一個頁面是 [完成精靈]。 您可在這個頁面上檢閱您在精靈中的選擇，然後啟動作業。 如需詳細資訊，請參閱[完成精靈](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md)。  
 
## <a name="see-also"></a>另請參閱  
[儲存套件](../../integration-services/save-packages.md)  
[執行 Integration Services (SSIS) 套件](../../integration-services/packages/run-integration-services-ssis-packages.md)  
[SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)
 
 