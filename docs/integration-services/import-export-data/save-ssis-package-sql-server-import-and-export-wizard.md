---
title: 儲存 SSIS 套件 (SQL Server 匯入和匯出精靈) | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: import-export-data
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.savedtspackage.f1
ms.assetid: 7bf8ac6a-5599-43ab-bf5c-e072c11b85a0
caps.latest.revision: 64
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3922b2e80e4597ed01f49c5766fce34c0d338e77
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="save-ssis-package-sql-server-import-and-export-wizard"></a>儲存 SSIS 封裝 (SQL Server 匯入和匯出精靈)
  如果您在 [儲存並執行套件] 頁面上指定要將設定儲存為 SQL Server Integration Services (SSIS) 套件，[[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈] 會顯示 [儲存 SSIS 套件]。 在此頁面上，您可以指定儲存精靈所建立套件的其他選項。  

您之前在 [儲存並執行封裝]  頁面上為將封裝儲存到 SQL Server 或檔案系統所執行的選擇，決定您在 [儲存 SSIS 封裝]  頁面中看到的選項。 若要再次查看 [儲存並執行封裝]  頁面，請參閱 [儲存並執行封裝](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)。
 
**什麼是套件？** 精靈使用 SQL Server Integration Services (SSIS) 複製資料。 在 SSIS 中，基本的單位就是封裝。 當您在精靈的頁面間移動並指定選項時，精靈會在記憶體中建立 SSIS 封裝。

## <a name="screen-shot---common-options"></a>螢幕擷取畫面 - 一般選項
下列螢幕擷取畫面顯示精靈的 [儲存 SSIS 套件] 頁面的第一個部分。 頁面的其餘部分具有不同數目的選項，而這取決於您選擇的套件目的地。

![儲存套件 - 一般選項](../../integration-services/import-export-data/media/save-package-common-options.png)

## <a name="provide-a-name-and-description-for-the-package"></a>提供套件的名稱和描述  
 **名稱**  
 提供封裝的唯一名稱。  
  
 **說明**  
 提供封裝的描述。 最佳作法是描述封裝用途，使封裝可以自我記錄並易於維護。  
  
 **目標**  
 您之前為套件指定的目的地 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或檔案系統)。 如果想將封裝儲存至不同的目的地，請返回 [儲存並執行封裝]  頁面。

## <a name="screen-shot---save-the-package-in-sql-server"></a>螢幕擷取畫面 - 將套件儲存在 SQL Server

 下列螢幕擷取畫面會在您於 [儲存並執行套件] 頁面上選取 [SQL Server] 選項時，顯示精靈的 [儲存 SSIS 套件] 頁面。 
  
![[匯入和匯出精靈] 的 [儲存 SSIS 套件] 頁面](../../integration-services/import-export-data/media/save-package2.png "[匯入和匯出精靈] 的 [儲存 SSIS 套件] 頁面")  

## <a name="options-to-specify-target--sql-server"></a>要指定的選項 (目標 = SQL Server) 

 > [!NOTE]
 > 精靈會將 **msdb** 資料庫的套件儲存至 **sysssispackages** 資料表。 此選項**不會**將套件儲存至 SSIS 目錄資料庫 (SSISDB)。  
 
 **伺服器名稱**  
 輸入或選取目的地伺服器名稱。  
   
 **[使用 Windows 驗證]**  
使用 Windows 整合式驗證連接到伺服器。 這是慣用的驗證方法。  
  
 **使用 SQL Server 驗證**  
使用 SQL Server 驗證連接到伺服器。  
  
 **User name**  
如果您已指定 SQL Server 驗證，請輸入使用者名稱。  
  
 **密碼**  
如果您已指定 SQL Server 驗證，請輸入密碼。  
    
## <a name="screen-shot---save-the-package-in-the-file-system"></a>螢幕擷取畫面 - 將套件儲存在檔案系統
 
下列螢幕擷取畫面會在您於 [儲存並執行套件] 頁面上選取 [檔案系統] 選項時，顯示精靈的 [儲存 SSIS 套件] 頁面。 
  
![[匯入和匯出精靈] 的 [儲存 SSIS 套件] 頁面](../../integration-services/import-export-data/media/save-package1.png "[匯入和匯出精靈] 的 [儲存 SSIS 套件] 頁面")  

## <a name="options-to-specify-target--file-system"></a>要指定的選項 (目標 = 檔案系統)

 **檔案名稱**  
 輸入目的地檔案的路徑和檔案名稱，或使用 [瀏覽] 按鈕選取目的地。  
  
> [!TIP]
> 請務必透過輸入或瀏覽方式指定目的地資料夾。 如果您只輸入檔案名稱而未輸入路徑，則不知道精靈儲存套件的位置。 此外，精靈也可能會嘗試將封裝儲存在您無權儲存檔案的位置，進而引發錯誤。  
>   
>  請記住封裝檔案的儲存位置。  
  
 **瀏覽**  
 選擇性地，在 [儲存套件] 對話方塊中，瀏覽以選取目的地檔案的路徑。  

## <a name="about-the-two-pages-of-options-for-saving-the-package"></a>有關儲存封裝選項的兩個頁面  
 [儲存 SSIS 封裝]  頁面是挑選用來儲存 SSIS 封裝選項的兩個頁面之一。  
  
-   在前一個 [Save and Execute Package (儲存並執行封裝)] 頁面中，您選擇將封裝儲存在 SQL Server 中或存為檔案。 您還可以為儲存的封裝選擇安全性設定。 若要再次查看 [儲存並執行封裝]  頁面，請參閱 [儲存並執行封裝](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)。  
  
-   在目前的頁面上，您提供封裝名稱以及儲存的詳細資訊。  
 
## <a name="run-the-saved-package-again-later"></a>稍後再次執行已儲存的封裝  
 若要了解稍後如何再次執行已儲存的封裝，請參閱下列主題之一。  
  
-   若要以具有好用的使用者介面的公用程式來執行封裝，請參閱[執行封裝公用程式 &#40;DtExecUI&#41; UI 參考](../../integration-services/packages/execute-package-utility-dtexecui-ui-reference.md)。  
  
-   若要從命令列或批次檔執行封裝，請參閱 [dtexec 公用程式](../../integration-services/packages/dtexec-utility.md)。  
  
-   如果是在 SQL Server 的 **msdb** 資料庫中儲存封裝，請連接到 Integration Services 服務。 然後，在 SQL Server Management Studio 的物件總管中，巡覽至 [存放的封裝 |MSDB] ，以滑鼠右鍵按一下封裝，然後選取 [執行封裝] 。

-   如果是在檔案系統中儲存封裝，請參閱 [執行 Integration Services (SSIS) 套件](../../integration-services/packages/run-integration-services-ssis-packages.md) 在開發環境中執行封裝。 您必須先將封裝加入 Integration Services 專案中，才能開啟並執行它。  

## <a name="customize-the-saved-package"></a>自訂已儲存的封裝  
 若要了解如何自訂已儲存的封裝，請參閱 [Integration Services &#40;SSIS&#41; 封裝](../../integration-services/integration-services-ssis-packages.md)。  
  
## <a name="whats-next"></a>下一步  
 指定儲存封裝的其他選項之後，下一個頁面是 [完成精靈] 。 您可在這個頁面上檢閱您在精靈中的選擇，然後啟動作業。 如需詳細資訊，請參閱 [完成精靈](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md)。  
 
## <a name="see-also"></a>另請參閱  
[儲存套件](../../integration-services/save-packages.md)  
[執行 Integration Services (SSIS) 套件](../../integration-services/packages/run-integration-services-ssis-packages.md)  
[SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)
 
 
