---
title: 設定模擬選項 (SSAS-多維度) |Microsoft 文件
ms.custom: ''
ms.date: 03/13/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.asvs.sqlserverstudio.impersonationinfo.f1
helpviewer_keywords:
- Impersonation Information dialog box
ms.assetid: 8e127f72-ef23-44ad-81e6-3dd58981770e
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 55ec66efd96a14bde8a9ea8b26488e18faadac0f
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="set-impersonation-options-ssas---multidimensional"></a>設定模擬選項 (SSAS - 多維度)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]建立時**資料來源**物件在 Analysis Services 模型中，您必須設定的設定值就是模擬選項。 此選項會決定當執行與連接有關的本機作業時，Analysis Services 是否採用特定 Windows 使用者帳戶的識別，例如在支援漫遊設定檔的環境中載入 OLE DB 資料提供者或解析使用者設定檔資訊。  
  
 如果是使用 Windows 驗證的連接，則模擬選項也會決定在外部資料來源執行查詢所使用的使用者識別。 例如，如果您將模擬選項設定為 **contoso\dbuser**，則在處理期間用來擷取資料的查詢將會以資料庫伺服器上的 **contoso\dbuser** 身分執行。  
  
 本主題說明在設定資料來源物件時，如何在 [模擬資訊] 對話方塊中設定模擬選項。  
  
## <a name="set-impersonation-options-in-sql-server-data-tools"></a>在 SQL Server Data Tools 中設定模擬選項  
  
1.  在 [方案總管] 中，按兩下資料來源開啟 [資料來源設計師]。  
  
2.  按一下 [資料來源設計師] 中的 [模擬資訊] 索引標籤。  
  
3.  選擇本主題的 [模擬選項](#bkmk_options) 所述的選項。  
  
## <a name="set-impersonation-options-in-management-studio"></a>在 Management Studio 中設定模擬選項  
 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，針對這些對話方塊的下列屬性按一下省略符號 (**...**) 按鈕，以開啟 [模擬資訊] 對話方塊：  
  
-   [資料庫屬性] 對話方塊，透過 [資料來源模擬資訊] 屬性。  
  
-   [資料來源屬性] 對話方塊，透過 [模擬資訊] 屬性。  
  
-   [組件屬性] 對話方塊，透過 [模擬資訊] 屬性。  
  
##  <a name="bkmk_options"></a> 模擬選項  
 對話方塊中的所有選項都可以使用，但並非所有選項都適合所有案例。 請使用下列資訊來確定最適合您案例的選項。  
  
 **使用特定的使用者名稱和密碼**  
 選取此選項即可讓[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]物件使用依照以下格式指定 Windows 使用者帳戶的安全性認證： *\<網域名稱 >*  **\\**  *\<使用者帳戶名稱 >*。  
  
 選擇此選項，即可使用您專為資料存取目的所建立的專用最低權限 Windows 使用者識別。 例如，如果您習慣建立一般用途帳戶來擷取報表中使用的資料，則可以在此指定該帳戶。  
  
 若為多維度資料庫，指定的認證將用於處理、ROLAP 查詢、非正規 (out-of-line) 繫結、本機 Cube、採礦模型、遠端資料分割、連結物件以及從目標到來源的同步處理。  
  
 若為 DMX OPENQUERY 陳述式，系統將忽略這個選項，並且使用目前使用者的認證，而非指定的使用者帳戶。  
  
 **使用服務帳戶**  
 選取此選項即可讓 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件使用與管理該物件之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服務相關聯的安全性認證。 這是預設選項。 在舊版中，這是您可以使用的唯一選項。 若要監視服務等級的資料存取，而不是個別使用者帳戶，建議您使用此選項。  
  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，服務帳戶可能是 NetworkService 或針對特定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體所建立的內建虛擬帳戶 (視您使用的作業系統而定)。 如果您針對使用 Windows 驗證的連接選擇此服務帳戶，請記得要為這個帳戶建立資料庫登入並授與讀取權限，因為它將在處理期間用來擷取資料。 如需服務帳戶的詳細資訊，請參閱[設定 Windows 服務帳戶和權限](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。  
  
> [!NOTE]  
>  當您使用資料庫驗證時，如果服務是在 Analysis Services 的專用虛擬帳戶之下執行，您應該選擇 [使用服務帳戶] 模擬選項。 此帳戶將具有存取本機檔案的權限。 如果此服務是以 NetworkService 身分執行，更好的替代方式是使用具有 [允許本機登入] 權限的最低權限 Windows 使用者帳戶。 根據您提供的帳戶而定，您可能也需要授與 Analysis Services 程式資料夾的檔案存取權限。  
  
 若為多維度資料庫，服務帳戶認證將用於處理、ROLAP 查詢、遠端資料分割、連結物件以及從目標到來源的同步處理。  
  
 若是 DMX OPENQUERY 陳述式、本機 Cube 和採礦模型，即使選擇服務帳戶選項，也會使用目前使用者的認證。 非正規 (out-of-line) 繫結不支援服務帳戶選項。  
  
> [!NOTE]  
>  如果服務帳戶沒有 Analysis Services 執行個體的管理員權限，則從 Cube 處理資料採礦模型時可能會發生錯誤。 如需詳細資訊，請參閱 [採礦結構：當資料來源為 OLAP Cube 時的處理問題](http://go.microsoft.com/fwlink/?LinkId=251610)。  
  
 **使用目前使用者的認證**  
 選取此選項即可讓 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件使用目前使用者的安全性認證來進行非正規 (out-of-line) 繫結、DMX OPENQUERY、本機 Cube 和採礦模型。  
  
 除了使用非正規 (out-of-line) 繫結的本機 Cube 和處理之外，多維度資料庫不支援這個選項。  
  
 **預設值**或**繼承**  
 此對話方塊會針對在資料庫層級設定的模擬選項使用 [預設值]，而針對在資料來源層級設定的模擬選項使用 [繼承]。  
  
 **資料來源 – 繼承選項**  
  
 在資料來源層級，[繼承] 會指定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 應該使用父物件的模擬選項。 在多維度模型中，父物件是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫。 選擇 [繼承] 選項，可讓您集中管理這個資料來源及屬於相同資料庫之其他資料來源的模擬設定。 您必須在資料庫層級選擇特定 Windows 使用者名稱和密碼，這個選項才有意義。 否則，在資料來源上使用 [繼承] 搭配在資料庫上使用 [預設值]，會相當於使用服務帳戶選項。  
  
 若要在資料庫層級指定 Windows 使用者名稱和密碼，請執行以下操作：  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，以滑鼠右鍵按一下資料庫，然後選取 [屬性]。  
  
2.  在 [資料來源模擬資訊] 中，指定 Windows 使用者名稱和密碼。  
  
3.  以滑鼠右鍵按一下每個資料來源，並檢視其屬性，以確保每個資料來源使用 [繼承] 選項。  
  
 如需資料庫層級之預設設定的詳細資訊，請參閱[設定多維度資料庫屬性 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/set-multidimensional-database-properties-analysis-services.md)。  
  
 **資料庫 – 預設選項**  

 若為多維度資料庫，[預設值] 表示使用服務帳戶和目前使用者進行資料採礦作業。  
  
## <a name="see-also"></a>請參閱  
 [建立資料來源 &#40;SSAS 多維度&#41;](../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)   
 [設定資料來源屬性 &#40;SSAS 多維度&#41;](../../analysis-services/multidimensional-models/set-data-source-properties-ssas-multidimensional.md)   

  
  
