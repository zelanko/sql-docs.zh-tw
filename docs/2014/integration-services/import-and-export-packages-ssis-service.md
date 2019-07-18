---
title: 匯入和匯出封裝 （SSIS 服務） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], importing
- packages [Integration Services], exporting
- importing packages
- exporting packages
ms.assetid: ef18ec11-b536-47d9-abd1-794099f43486
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9a1d50afde56843942c470017a8534ffa797eb69
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66058144"
---
# <a name="import-and-export-packages-ssis-service"></a>匯入和匯出封裝 (SSIS 服務)
    
> [!IMPORTANT]  
>  本主題會討論 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務，即用於管理 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝的 Windows 服務。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 支援此服務能與舊版 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]回溯相容。 從 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]開始，您可以管理 Integration Services 伺服器上的物件，例如封裝。  
  
 封裝可以儲存在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb 資料庫的 sysssispackages 資料表中，也可以儲存在檔案系統中。  
  
 封裝存放區 ([!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務所監視和管理的邏輯儲存體) 可以同時包含在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務之組態檔中指定的 msdb 資料庫和檔案系統資料夾。  
  
 您可以在下列儲存體類型之間匯入和匯出封裝：  
  
-   檔案系統中任意位置的檔案系統資料夾。  
  
-   「SSIS 封裝存放區」中的資料夾。 兩個預設資料夾名為 File System 和 MSDB。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] msdb 資料庫。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 可讓您匯入和匯出封裝，並藉此變更封裝的儲存格式和位置。 使用匯入和匯出功能，可以將封裝加入檔案系統、封裝存放區或 msdb 資料庫，並將封裝從一個儲存體複製到另一個儲存體。 例如，可以將 msdb 中儲存的封裝複製到檔案系統，反之亦然。  
  
 您也可以使用 **dtutil** 命令提示公用程式 (dtutil.exe)，將封裝複製成其他格式。 如需詳細資訊，請參閱 [dtutil Utility](dtutil-utility.md)。  
  
## <a name="to-import-or-export-a-package"></a>匯入或匯出封裝  
  
> [!IMPORTANT]  
>  本主題會討論 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 的 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]服務。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 支援 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務，可回溯相容於 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]。 如需在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中管理封裝的資訊，請參閱 [Integration Services &#40;SSIS&#41; 伺服器](catalog/integration-services-ssis-server-and-catalog.md)。  
  
 您可以在下列位置之間匯入或匯出 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝：  
  
-   您可以匯入儲存在 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體、檔案系統或 [!INCLUDE[ssIS](../includes/ssis-md.md)] 封裝存放區內的封裝。 匯入的封裝將儲存到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssIS](../includes/ssis-md.md)] 封裝存放區內的資料夾中。  
  
-   您可以將儲存在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體、檔案系統或 [!INCLUDE[ssIS](../includes/ssis-md.md)] 封裝存放區內的封裝匯出至不同的儲存格式和位置。  
  
 不過，在不同的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本之間匯入和匯出封裝有一些限制：  
  
-   在 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 的執行個體上，雖然您可以從 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 的執行個體匯入封裝，但是無法將封裝匯出至 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 的執行個體。  
  
-   在 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] 的執行個體上，您無法在 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 的執行個體之間匯入封裝或匯出封裝。  
  
 下列程序將描述如何使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 來匯入或匯出封裝。  
  
#### <a name="to-import-a-package-by-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 來匯入封裝  
  
1.  按一下 [開始]  、指向 [Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]]  ，然後按一下 [SQL Server Management Studio]  。  
  
2.  在 [連接到伺服器]  對話方塊上，設定下列選項：  
  
    -   在 [伺服器類型]  方塊中，選取 [Integration Services]  。  
  
    -   在 [伺服器名稱]  方塊中提供伺服器名稱，或按一下 [\<瀏覽其他...>]  ，並尋找要使用的伺服器。  
  
3.  如果物件總管尚未開啟，請在 [檢視]  功能表上，按一下物件總管  。  
  
4.  在物件總管中，展開 [存放的封裝]  資料夾。  
  
5.  展開子資料夾以尋找您要匯入封裝的資料夾。  
  
6.  以滑鼠右鍵按一下資料夾，然後按一下 [匯入封裝]  。 然後執行下列其中之一：  
  
    -   若要從 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體匯入，請選取 [SQL Server]  選項，然後指定伺服器並選取驗證模式。 如果選取 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證，請提供使用者名稱和密碼。  
  
         按一下瀏覽按鈕 ([...])  ，選取要匯入的封裝，然後按一下 [確定]  。  
  
    -   若要從檔案系統匯入，請選取 [檔案系統]  選項。  
  
         按一下瀏覽按鈕 ([...])  ，選取要匯入的封裝，然後按一下 [開啟]  。  
  
    -   若要從 [!INCLUDE[ssIS](../includes/ssis-md.md)] 封裝存放區匯入，請選取 [SSIS 封裝存放區]  選項並指定伺服器。  
  
         按一下瀏覽按鈕 ([...])  ，選取要匯入的封裝，然後按一下 [確定]  。  
  
7.  (選擇性) 更新封裝名稱。  
  
8.  若要更新封裝的保護等級，請按一下瀏覽按鈕 ([...])  ，並使用 [封裝保護等級]  對話方塊選擇其他保護等級。 如果選取 [機密資料以密碼加密]  或 [所有資料以密碼加密]  選項，請鍵入並確認密碼。  
  
9. 按一下 [確定]  以完成匯入。  
  
#### <a name="to-export-a-package-by-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 來匯出封裝  
  
1.  按一下 [開始]  、指向 [Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]]  ，然後按一下 [SQL Server Management Studio]  。  
  
2.  在 [連接到伺服器]  對話方塊上，設定下列選項：  
  
    -   在 [伺服器類型]  方塊中，選取 [Integration Services]  。  
  
    -   在 [伺服器名稱]  方塊中提供伺服器名稱，或按一下 [\<瀏覽其他...>]  ，並尋找要使用的伺服器。  
  
3.  如果物件總管尚未開啟，請在 [檢視]  功能表上，按一下物件總管  。  
  
4.  在物件總管中，展開 [存放的封裝]  資料夾。  
  
5.  展開子資料夾，以找出您要匯出的封裝。  
  
6.  以滑鼠右鍵按一下封裝，再按一下 [匯出]  ，然後執行下列其中之一：  
  
    -   若要匯出至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體，請選取 [SQL Server]  選項，然後指定伺服器並選取驗證模式。 如果選取 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證，請提供使用者名稱和密碼。  
  
         按一下瀏覽按鈕 ([...])  並展開 [SSIS 封裝]  資料夾，以找出您要儲存封裝的資料夾。 (選擇性) 更新封裝的預設名稱並按一下 [確定]  。  
  
    -   若要匯出至檔案系統，請選取 [檔案系統]  選項。  
  
         按一下瀏覽按鈕 ([...])  找出您要匯出封裝的目標資料夾、輸入封裝檔案的名稱，然後按一下 [儲存]  。  
  
    -   若要匯出至 [!INCLUDE[ssIS](../includes/ssis-md.md)] 封裝存放區，請選取 [SSIS 封裝存放區]  選項，並指定伺服器。  
  
         按一下瀏覽按鈕 ([...])  ，展開 [SSIS 封裝]  資料夾，並選取您要儲存封裝的資料夾。 (選擇性) 在 [封裝名稱]  文字方塊中輸入封裝的新名稱。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  若要更新封裝的保護等級，請按一下瀏覽按鈕 ([...])  ，並使用 [封裝保護等級]  對話方塊選擇其他保護等級。 如果選取 [機密資料以密碼加密]  或 [所有資料以密碼加密]  選項，請鍵入並確認密碼。  
  
8.  按一下 [確定]  以完成匯出。  
  
## <a name="see-also"></a>另請參閱  
 [封裝管理 &#40;SSIS 服務&#41;](service/package-management-ssis-service.md)  
  
  
