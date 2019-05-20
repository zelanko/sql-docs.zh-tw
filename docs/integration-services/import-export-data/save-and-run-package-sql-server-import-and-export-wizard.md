---
title: 儲存並執行套件 (SQL Server 匯入和匯出精靈) | Microsoft Docs
ms.custom: ''
ms.date: 02/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.saveschedule.f1
ms.assetid: b582c462-3d7a-4a4c-a2a2-2c79fedab75a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8326920e557d6ed304414f96a7da040de0093dd0
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2019
ms.locfileid: "65723731"
---
# <a name="save-and-run-package-sql-server-import-and-export-wizard"></a>儲存並執行套件 (SQL Server 匯入和匯出精靈)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  在您指定及設定資料來源和目的地之後，[ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 匯入和匯出精靈] 會顯示 [儲存並執行封裝] 。 在此頁面上，您可以指定是否要立即執行複製作業。 根據您的設定，也可以將設定儲存為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (SSIS) 套件進行自訂並在稍後重複使用。
  
**什麼是套件？** 精靈使用 SQL Server Integration Services (SSIS) 複製資料。 在 SSIS 中，基本的單位就是封裝。 當您在精靈的頁面間移動並指定選項時，精靈會在記憶體中建立 SSIS 封裝。
  
## <a name="screen-shot-of-the-save-and-run-package-page"></a>[儲存並執行套件] 頁面的螢幕擷取畫面  
下列螢幕擷取畫面顯示精靈的 [儲存並執行封裝]  頁面。 
   
![[匯入和匯出精靈] 的 [儲存並執行套件] 頁面](../../integration-services/import-export-data/media/save-and-run.png "[匯入和匯出精靈] 的 [儲存並執行套件] 頁面") 
  
## <a name="run-and-save-the-package"></a>儲存並執行套件 
 您必須至少選取下列兩個選項之一才能繼續。  
  
 **Run immediately**  
 選取此選項，立即匯入和匯出資料。 預設會選取此核取方塊，並立即執行作業。
  
 **儲存 SSIS 套件**  
 將設定儲存為 SSIS 套件。 稍後您可以選擇自訂封裝，再執行一次。 如果您選擇儲存封裝，下一個頁面 [儲存 SSIS 封裝] 上還有其他選項。
 
只有在您已安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard Edition 或更新版本時，才能使用儲存封裝的選項。   
  
> [!NOTE]
> 如果您完成精靈，並執行作業，但在執行完成之前停止作業，則不會儲存套件，即使您選取 [儲存 SSIS 套件] 核取方塊也是一樣。  

### <a name="if-you-started-the-wizard-from-visual-studio"></a>如果您已從 Visual Studio 啟動精靈
如果您已使用 SQL Server Data Tools (SSDT) 從 Visual Studio 的 Integration Services 專案啟動精靈：
-   在結束精靈之前，您無法「執行」套件。 然後您可以從 Visual Studio 執行套件。
-   精靈會將套件「儲存」至可從中啟動精靈的 Integration Services 專案。

## <a name="specify-options-for-saving-the-package"></a>指定儲存套件的選項
**SQL Server**  
 選取此選項，以將 **msdb** 資料庫的 SQL Server 中的套件儲存至 **sysssispackages** 資料表。
 
> [!IMPORTANT]
> 這個選項不會將封裝儲存在 SSIS 目錄資料庫 (SSISDB) 中。  

 您可以在下一個頁面 [儲存 SSIS 封裝] 上，選取目標伺服器並提供認證以連接到伺服器。 如需詳細資訊，請參閱 [儲存 SSIS 封裝](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)。  
  
 **檔案系統**  
 選取此選項，即可將套件儲存為副檔名為 **.dtsx** 的檔案。  
  
 您可以在下一個頁面 [儲存 SSIS 封裝] 上，選取封裝的目標資料夾和檔案名稱。 如需詳細資訊，請參閱 [儲存 SSIS 封裝](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)。  
 
 ## <a name="specify-the-package-protection-level"></a>指定套件保護等級
 **套件保護層級**  
 從清單中選取保護層級，以協助保護封裝中的資料。  
  
 保護等級會決定保護方法、密碼或使用者金鑰，以及封裝保護的範圍。 保護可包括所有資料或只包括機密資料。 如需可用選項的詳細資訊，請參閱 [封裝中的敏感性資料存取控制](../../integration-services/security/access-control-for-sensitive-data-in-packages.md)。  
  
 **密碼**  
 輸入密碼。  
  
 **再次輸入密碼**  
 再輸入密碼一次。  
  
> [!NOTE]
> 只有指定需要密碼的 [套件保護等級] (亦即，指定 [機密資料以密碼加密] 或 [所有資料以密碼加密] 時)，才有密碼選項可用。  

## <a name="about-the-two-pages-of-options-for-saving-the-package"></a>有關儲存封裝選項的兩個頁面  
 [儲存並執行封裝]  頁面是選擇用來儲存 SSIS 封裝選項的兩個頁面之一。  
  
-   在目前的頁面上，您可以選擇要將封裝儲存在 SQL Server 中或另存為檔案。 您還可以為儲存的封裝選擇安全性設定。  
  
-   接下來，在 [儲存 SSIS 封裝]  頁面上，您可以提供封裝的名稱及儲存位置的詳細資訊。 如需詳細資訊，請參閱 [儲存 SSIS 封裝](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)。  
  
 只有在您選取此頁面上的 [儲存 SSIS 封裝]  選項時，才能使用這些選項。  
  
## <a name="whats-next"></a>下一步  
 在您指定是否要立即執行複製作業及是否要儲存封裝之後，下一個頁面取決於您選擇的選項。  
  
-   如果您選取了立即執行封裝但不儲存的選項，下一個頁面會是 [完成精靈] 。 在此頁面上，您可以檢閱在精靈中的選擇，然後開始複製作業。 如需詳細資訊，請參閱 [完成精靈](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md)。  
  
-   如果您選取了儲存封裝的選項，下一個頁面會是 [儲存 SSIS 封裝] 。 在此頁面上，您可以指定儲存封裝的其他選項 (然後，在儲存封裝之後，下一個頁面是 [完成精靈])。如需詳細資訊，請參閱[儲存 SSIS 封裝](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)。  
  
## <a name="see-also"></a>另請參閱  
[儲存套件](../../integration-services/save-packages.md)  
[執行 Integration Services (SSIS) 套件](../../integration-services/packages/run-integration-services-ssis-packages.md)  
[SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
[透過匯入和匯出精靈的簡單範例開始使用](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)

  

