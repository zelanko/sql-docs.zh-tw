---
title: 使用公用程式總管來管理 SQL Server 公用程式 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 74012c90-b42e-4171-b27a-9c30cf69ff98
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 232beed45a62ad9cef9f43b122d23cb4d0728a78
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63191710"
---
# <a name="use-utility-explorer-to-manage-the-sql-server-utility"></a>使用公用程式總管來管理 SQL Server 公用程式
  公用程式總管是 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的元件，它會連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體，以便在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式內提供所有物件的樹狀檢視。 [公用程式總管] 內容窗格會提供幾個方法來檢視摘要與詳細資料，並提供與 SQL Server 受管理的執行個體健全狀態相關的資料。 [公用程式總管] 也會提供用於檢視及管理原則定義的使用者介面。 公用程式總管的功能會因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式內的物件而有些微的不同，但是一般來說都會包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式所管理的物件、資料和原則。 如需詳細資訊，請參閱 [SQL Server 公用程式的功能與工作](sql-server-utility-features-and-tasks.md)。  
  
## <a name="create-utility-control-point"></a>建立公用程式控制點  
 在您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式之前，您必須建立公用程式控制點。 如需詳細資訊，請參閱 [SQL Server 公用程式的功能與工作](sql-server-utility-features-and-tasks.md)或[建立 SQL Server 公用程式控制點 &#40;SQL Server 公用程式&#41;](create-a-sql-server-utility-control-point-sql-server-utility.md)。  
  
## <a name="enroll-an-instance-of-sql-server-or-a-data-tier-application-from-utility-explorer"></a>從公用程式總管註冊 SQL Server 執行個體或資料層應用程式  
 您可以輕鬆地將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體註冊到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式。 在公用程式總管中，以滑鼠右鍵按一下 **[受管理的執行個體]** 節點，然後按一下 **[新增受管理的執行個體]** 。 遵循精靈的步驟完成作業。 如需詳細資訊，請參閱[註冊 SQL Server 的執行個體 &#40;SQL Server 公用程式&#41;](enroll-an-instance-of-sql-server-sql-server-utility.md)。  
  
 若要在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式內將資料層應用程式部署到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受管理的執行個體，請按一下 [物件總管]  索引標籤，並展開 [管理]  節點，然後以滑鼠右鍵按一下 [資料層應用程式]  。 從滑鼠右鍵功能表中，選取 [部署資料層應用程式]  。 如需詳細資訊，請參閱[部署資料層應用程式](../data-tier-applications/deploy-a-data-tier-application.md)。  
  
## <a name="viewing-utility-explorer"></a>檢視公用程式總管  
 預設在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中看不到公用程式總管。 如果您在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 使用者介面中看不到公用程式總管，請在 **[檢視]** 功能表上按一下 **[公用程式總管]** 。 若要檢視 [公用程式總管] 內容窗格，請在 **[檢視]** 功能表上按一下 **[公用程式總管內容]** 。  
  
## <a name="viewing-objects-in-utility-explorer"></a>在公用程式總管中檢視物件  
 [公用程式總管] 導覽窗格和 [公用程式總管] 內容窗格會顯示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式所管理的資料、物件和原則。 使用此導覽窗格可指定要顯示在儀表板和視點中的資訊，然後使用此內容窗格和詳細資料索引標籤可存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式所管理之物件的資料和原則資訊。  
  
### <a name="sql-server-utility-navigation-pane"></a>SQL Server 公用程式導覽窗格  
 [公用程式總管] 導覽窗格會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式內提供物件的樹狀檢視 (以公用程式控制點來分組)。 若要展開資料夾，請在 [公用程式總管] 導覽窗格內按一下加號 (+) 或是按兩下 UCP 名稱。 以滑鼠右鍵按一下資料夾或物件來執行一般工作。 樹狀檢視中的節點如下所示：  
  
-   樹狀檢視中的最上層節點為公用程式控制點 (UCP)， 節點名稱會建構為："Utility_Name"(ComputerName\UCP_instance_name)。 如果您沒有 UCP，則必須建立 UCP。 如果您未連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式，必須建立一個連接。 如需詳細資訊，請參閱 [SQL Server 公用程式的功能與工作](sql-server-utility-features-and-tasks.md)。 在樹狀檢視中按一下 UCP 名稱，使用儀表板檢視中的資料來填入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 [公用程式總管] 內容窗格。 如需詳細資訊，請參閱[公用程式儀表板 &#40;SQL Server 公用程式&#41;](../../database-engine/utility-dashboard-sql-server-utility.md)。  
  
     以滑鼠右鍵按一下 UCP 節點以重新整理儀表板中的資料。  
  
-   在樹狀檢視中按一下 **[部署的資料層應用程式]** 節點，存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式內容窗格中的清單檢視資料。 內容窗格底部的詳細資料索引標籤會提供 CPU 和儲存使用量的資料，以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式內個別資料層應用程式之原則定義和屬性詳細資料的存取權。 如需詳細資訊，請參閱[部署的資料層應用程式詳細資料 &#40;SQL Server 公用程式&#41;](../../database-engine/deployed-data-tier-application-details-sql-server-utility.md)。  
  
     在樹狀檢視中以滑鼠右鍵按一下 [部署的資料層應用程式]  節點，以存取篩選設定或重新整理清單檢視中的資料。  
  
-   在樹狀檢視中按一下 **[受管理的執行個體]** 節點，以存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式內容窗格中的清單檢視資料。 內容窗格底部的詳細資料索引標籤會提供 CPU 與存放磁碟區使用量的資料，以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式內個別 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受管理的執行個體之原則定義與屬性詳細資料的存取權。 如需詳細資訊，請參閱[受管理的執行個體詳細資料 &#40;SQL Server 公用程式&#41;](../../database-engine/managed-instance-details-sql-server-utility.md)。  
  
     在樹狀檢視中以滑鼠右鍵按一下 [受管理的執行個體]  節點，將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的受管理執行個體加入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式中，以存取篩選設定或重新整理清單檢視中的資料。  
  
-   按一下樹狀檢視中的 [公用程式管理]  節點，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式中針對所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受管理執行個體及部署的資料層應用程式來存取全域原則定義，以檢視 UCP 管理員資訊，並存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式管理資料倉儲的組態設定。 如需詳細資訊，請參閱[公用程式管理 &#40;SQL Server 公用程式&#41;](../../database-engine/utility-administration-sql-server-utility.md)。 您也可以使用 **[原則]** 索引標籤上的控制項，變更報告原則違規的敏感度。 如需詳細資訊，請參閱[降低 CPU 使用量原則的雜訊 &#40;SQL Server Utility&#41;](reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)。  
  
     在樹狀檢視中，以滑鼠右鍵按一下 [公用程式管理]  節點，以重新整理內容窗格中的資料。  
  
### <a name="sql-server-utility-dashboard"></a>SQL Server 公用程式儀表板  
 在 [公用程式總管] 樹狀檢視中選取 UCP 節點會填入 [公用程式總管] 內容窗格中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式儀表板。 此儀表板在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式內針對所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 受管理的執行個體和資料層應用程式提供其狀態的摘要，以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式所管理之物件的整體儲存使用量。 如需詳細資訊，請參閱[公用程式儀表板 &#40;SQL Server 公用程式&#41;](../../database-engine/utility-dashboard-sql-server-utility.md)。 若要註冊或移除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體，請參閱[註冊 SQL Server 的執行個體 &#40;SQL Server 公用程式&#41;](enroll-an-instance-of-sql-server-sql-server-utility.md) 或[部署資料層應用程式](../data-tier-applications/deploy-a-data-tier-application.md)或[從 SQL Server 公用程式移除 SQL Server 執行個體](remove-an-instance-of-sql-server-from-the-sql-server-utility.md)。  
  
### <a name="filtering-the-list-of-objects-in-utility-explorer-contents"></a>在公用程式總管內容中篩選物件清單  
 當節點包含大量物件時，可能很不容易找到您要找的物件。 在這種情況下，請利用 [公用程式總管] 的篩選功能來縮減清單大小。 例如，當您需要尋找特定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，或是只需要尋找檔案空間使用量過低的電腦時。 請以滑鼠右鍵按一下您要篩選的資料夾，再按一下篩選按鈕，然後按一下 **[篩選設定]** 來開啟 [公用程式總管篩選設定] 對話方塊。 您可以依名稱、電腦 CPU、執行個體 CPU、檔案空間、磁碟區空間、原則覆寫設定或上次報告時間來篩選清單。 **[運算子]** 和 **[值]** 資料行會在下拉式清單中提供其他篩選運算子。  
  
### <a name="starting-powershell"></a>啟動 PowerShell  
 您可以啟動 PowerShell 工作階段，其方式是以滑鼠右鍵按一下 [物件總管] 樹狀結構中的大多數資料夾和物件，然後選取 **[啟動 PowerShell]** 。 這樣會啟動 Powershell 工作階段，此工作階段已啟用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Powershell 支援，而且路徑會設定為您在 [物件總管] 中以滑鼠右鍵按一下的物件。 然後您可以在互動式 Powershell 環境中輸入 Powershell 命令。 如需詳細資訊，請參閱 [SQL Server PowerShell](../../powershell/sql-server-powershell.md)。  
  
 Powershell 沒有 F1 說明，但是它包含 **Get-Help** 指令程式，此指令程式提供 Powershell 的使用資訊。 如需使用 Get-Help 的詳細資訊，請參閱 [Get Help SQL Server PowerShell](../../database-engine/get-help-sql-server-powershell.md)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 公用程式的功能與工作](sql-server-utility-features-and-tasks.md)   
 [設定健全狀況原則 &#40;SQL Server 公用程式&#41;](configure-health-policies-sql-server-utility.md)   
 [物件總管](../../ssms/object/object-explorer.md)  
  
  
