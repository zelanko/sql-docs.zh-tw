---
title: 使用報表管理員建立模型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report models [Reporting Services], creating
- Report Manager [Reporting Services], model creation
ms.assetid: 8e5d2bd3-48ec-45f3-afee-6d86797c8f28
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7b67e2a7048520d8a411789e501dbbe545d3cc02
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109666"
---
# <a name="create-a-model-using-report-manager"></a>使用報表管理員建立模型
  您可以使用報表管理員，從 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Cube、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫或 Oracle 資料庫產生模型。 報表模型是從在報表伺服器上發行的共用資料來源產生的。 如果您還沒有共用資料來源，則必須建立一個。  
  
 您產生的報表模型是完全以共用資料來源的結構描述為基礎。 您無法選擇模型中要包含資料來源的哪些部分，也無法編輯產生之模型的規則或中繼資料。 但是，您可以在產生模型後設定模型的屬性，以及定義限制對模型全部或部分之存取的角色指派。  
  
> [!NOTE]  
>  Oracle 為基礎的模型產生使用報表管理員或[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[offSPServ](../includes/offspserv-md.md)] 2007年[!INCLUDE[SPS2010](../includes/sps2010-md.md)]會包含屬於用來連接到 Oracle 資料來源的使用者帳戶的結構描述的資料庫物件。 使用者帳戶名稱會在資料來源屬性認證中指定。  
  
### <a name="to-create-a-new-data-source-for-a-report-model-using-report-manager"></a>使用報表管理員建立報表模型的新資料來源  
  
1.  在網頁瀏覽器的網址列中，輸入報表伺服器的 URL。  
  
2.  按一下 **[新增資料來源]** 。  
  
3.  在 **[名稱]** 方塊中，輸入資料來源的名稱。  
  
4.  選擇性，在 **[描述]** 文字方塊中輸入模式的簡短描述。  
  
5.  確認已經選取 **[啟用此資料來源]** 核取方塊。  
  
6.  在 **[連接類型]** 清單中，選取您要連接的資料來源類型。 連接類型必須是下列其中一項：**Oracle**， **Microsoft SQL Server**或是**Microsoft SQL Server Analysis Services**。  
  
7.  在 **[連接字串]** 方塊中，輸入指向資料庫的連接字串。  
  
8.  選取報表產生器使用者需要用來連接到資料庫的連接方法。  
  
    -   Windows 驗證：選取此選項，當您想要驗證的作業系統時[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用者。 此選項允許 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 使用 Windows 安全性功能 (例如密碼加密)，來驗證使用者。 強烈建議您選取此選項。  
  
    -   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 驗證：選取此選項，當您想要使用的使用者時[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]您所建立的登入帳戶。 使用者必須提供有效的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 登入名稱和密碼。  
  
        > [!CAUTION]  
        >  可能的話，請使用 Windows 驗證。  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-create-a-report-model-using-report-manager"></a>使用報表管理員建立報表模型  
  
1.  在報表管理員中，選取您要用於模型的資料來源。  
  
     就會出現 [屬性] 頁面。  
  
2.  確認您要使用為資料來源指定的選項。  
  
3.  按一下 **[產生模型]** 。  
  
     就會顯示資料來源的 [一般] 頁面。  
  
4.  在 **[名稱]** 方塊中，輸入報表模型的名稱。  
  
5.  在 **[描述]** 方塊中，輸入模型的簡短描述。  
  
6.  若要指定儲存報表模型的新位置，請按一下 **[變更位置]** 。  
  
     依預設，報表模型是儲存在報表管理員的主資料夾。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     接著會建立報表模型，並將模型儲存到您指定的位置。 您可以使用「報表管理員」來為這個模型指派權限。  
  
## <a name="see-also"></a>另請參閱  
 [在原生模式報表伺服器上授與權限](security/granting-permissions-on-a-native-mode-report-server.md)   
 [資料連接、 資料來源和 Reporting Services 中的連接字串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [新增資料來源頁面 &#40;報表管理員&#41;](../../2014/reporting-services/new-data-source-page-report-manager.md)  
  
  
