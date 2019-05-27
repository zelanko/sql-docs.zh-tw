---
title: 授與 cube 或模型權限 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.roledesignerdialog.cubes.f1
helpviewer_keywords:
- user access rights [Analysis Services], cubes
- cubes [Analysis Services], security
- read/write permissions
- permissions [Analysis Services], cubes
ms.assetid: 55b1456e-2f6b-4101-b316-c926f40304e3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 12eb2a2f6ea7501e03830724b24c5808375db7c4
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66075031"
---
# <a name="grant-cube-or-model-permissions-analysis-services"></a>授與 Cube 或模型權限 (Analysis Services)
  Cube 或表格式模型是 Analysis Services 資料模型中的主要查詢物件。 從 Excel 連線到多維度或表格式資料以進行特定資料瀏覽時，使用者一開始通常會選取特定 Cube 或表格式模型做為樞紐分析報表物件後面的資料結構。 這個主題說明如何授與存取 Cube 或表格式資料的必要權限。  
  
 根據預設，除了伺服器管理員或資料庫管理員之外，其他人都不具備查詢資料庫中之 Cube 的權限。 非管理員的使用者存取 Cube 時，需要在針對包含 Cube 的資料庫建立的角色中擁有成員資格。 Windows 使用者或群組帳戶支援成員資格，這些帳戶是在 Active Directory 或本機電腦上定義。 開始之前，請先識別將把您即將建立之角色中的成員資格指派給哪些帳戶。  
  
 具有 Cube 的 `Read` 存取權也可以傳遞維度、量值群組及其中之檢視方塊的權限。 大部分的管理員將在 Cube 層級授與讀取權限，然後在特定物件上、相關聯的資料上，或者依據使用者識別限制權限。  
  
 若要在後續解決方案部署中保留角色定義，最佳做法是在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中定義角色來做為模型的一部分，然後讓資料庫管理員在發佈資料庫之後，於 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中指派角色成員資格。 但是，您可以針對這兩個工作使用其中一項工具。 為了簡化練習，我們將同時針對角色定義和成員資格使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。  
  
> [!NOTE]  
>  只有伺服器管理員或擁有完整控制權限的資料庫管理員可以將 Cube 從來源檔案部署到伺服器，或者建立角色並指派成員。 請參閱[授與伺服器系統管理員權限&#40;Analysis Services&#41; ](../instances/grant-server-admin-rights-to-an-analysis-services-instance.md)並[授與資料庫權限&#40;Analysis Services&#41; ](grant-database-permissions-analysis-services.md)如需這些權限的詳細資訊層級。  
  
#### <a name="step-1-create-the-role"></a>步驟 1:建立角色  
  
1.  在 SSMS 中，連線到 Analysis Services。 如果您需要這個步驟的說明，請參閱[從用戶端應用程式連接 &#40;Analysis Services&#41;](../instances/connect-from-client-applications-analysis-services.md)。  
  
2.  在物件總管中，開啟 [資料庫] 資料夾，然後選取資料庫。  
  
3.  以滑鼠右鍵按一下 [角色]，並選取 [新增角色]。 請注意，角色是在資料庫層級建立，並適用於其內部的物件。 您無法跨資料庫共用角色。  
  
4.  在 [一般] 窗格中，輸入名稱，並選擇性地輸入描述。 這個窗格也包含數個資料庫權限，例如，[完整控制權]、[處理資料庫] 及 [讀取定義]。 查詢 Cube 或表格式模型時不需要這些權限的任何一個。 如需這些權限的詳細資訊，請參閱[授與資料庫權限 &#40;Analysis Services&#41;](grant-database-permissions-analysis-services.md)。  
  
5.  輸入名稱和選擇性描述之後，請繼續下一個步驟。  
  
#### <a name="step-2-assign-membership"></a>步驟 2:指派成員資格  
  
1.  在 [成員資格] 窗格中，按一下 [新增]，以輸入將使用這個角色存取 Cube 的 Windows 使用者或群組帳戶。 Analysis Services 僅支援 Windows 安全性識別。 請注意，您不會在這個步驟中建立資料庫登入。 在 Analysis Services 中，使用者是透過 Windows 帳戶連線。  
  
2.  繼續下一個步驟，設定 Cube 權限。  
  
     請注意，我們正略過 [資料來源] 窗格。 大部分 Analysis Services 資料的一般取用者不需具備資料來源物件的權限。 如需這些權限層級的詳細資訊，請參閱 [授與資料來源物件的權限 &#40;Analysis Services&#41;](grant-permissions-on-a-data-source-object-analysis-services.md) 。  
  
#### <a name="step-3-set-cube-permissions"></a>步驟 3：設定 Cube 權限  
  
1.  在 [ **Cube** ] 窗格中，選取 cube，然後按一下`Read`或是**讀/寫**存取。  
  
     `Read` 存取就足以執行大部分的作業。 [讀取/寫入] 僅適用於回寫，不適用於處理。 如需此功能的詳細資訊，請參閱[設定分割區回寫](set-partition-writeback.md)。  
  
     請注意，您可以選取多個 Cube，以及可以在 [建立角色] 對話方塊中取得的其他物件。 授與存取 Cube 的權限會授權對與 Cube 相關聯之維度及檢視方塊的存取權。 不需要手動新增 Cube 中已經有的物件。  
  
     如果您需要根據物件或使用者來變更授權 (例如，讓特定量值變成無法使用)，您可以自動允許或拒絕特定物件 (甚至是資料格) 的存取權。 如需詳細資訊，請參閱[授與維度資料的自訂存取權 &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md) 和[授與資料格資料的自訂存取權 &#40;Analysis Services&#41;](grant-custom-access-to-cell-data-analysis-services.md)。  
  
2.  此時，當您按一下 [確定] 之後，這個角色的所有成員都會在您指定的權限層級上擁有 Cube 的存取權。  
  
     請注意，在 [Cube] 窗格中，您可以透過 [鑽研和本機 Cube] 權限授與使用者從伺服器 Cube 建立本機 Cube 的權限，或透過 [鑽研] 權限，授與使用者僅允許鑽研的權限。  
  
     最後，這個窗格可讓您授與 Cube 的 [處理資料庫] 權限，讓這個角色的所有成員都能夠處理這個 Cube 的資料。 因為處理通常是受限制的作業，所以建議您將這個工作留給管理員，或者特別針對該工作定義個別角色。 如需處理權限最佳做法的詳細資訊，請參閱[授與處理權限 &#40;Analysis Services&#41;](grant-process-permissions-analysis-services.md)。  
  
#### <a name="step-4-test"></a>步驟 4：測試  
  
1.  使用 Excel 測試 Cube 存取權限。 您也可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，後面接著以下所述的相同技術 - 以非管理員的使用者身分執行應用程式。  
  
    > [!NOTE]  
    >  如果您是 Analysis Services 管理員，管理員權限將是由擁有較少權限的角色所組成，因而很難獨立測試角色權限。 若要簡化測試，建議您使用指派給您正在測試之角色的帳戶，來開啟 SSMS 的第二個執行個體。  
  
2.  按住 Shift 鍵並以滑鼠右鍵按一下 [Excel] 捷徑，即可存取 [以不同的使用者身分執行] 選項。 輸入其中一個在此角色中擁有成員資格的 Windows 使用者或群組帳戶。  
  
3.  當 Excel 開啟時，請使用 [資料] 索引標籤來連線 Analysis Services。 因為您正以不同的 Windows 使用者身分執行 Excel，所以，[使用 Windows 驗證] 選項是在測試角色時要使用的正確認證類型。 如果您需要這個步驟的說明，請參閱[從用戶端應用程式連接 &#40;Analysis Services&#41;](../instances/connect-from-client-applications-analysis-services.md)。  
  
     如果您在連線時發生錯誤，請檢查適用於 Analysis Services 的連接埠設定，並確認伺服器接受遠端連線。 如需連接埠設定，請參閱 [設定 Windows 防火牆以允許 Analysis Services 存取](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md) 。  
  
#### <a name="step-5-script-role-definition-and-assignments"></a>步驟 5：指令碼角色定義和指派  
  
1.  在最後一個步驟中，您應該產生指令碼，來擷取您剛剛建立的角色定義。  
  
     從 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 重新部署專案將會覆寫任何未在專案內部定義的角色或角色成員資格。 在重新部署之後重建角色和角色成員資格的最快方式是透過指令碼。  
  
2.  請在 SSMS 中，瀏覽到 [角色] 資料夾，然後以滑鼠右鍵按一下現有角色。  
  
3.  選取 [編寫角色的指令碼] | [CREATE TO (CREATE 至)] | [檔案]。   
  
4.  使用 .xmla 副檔名來儲存檔案。 若要測試指令碼，請刪除目前角色、在 SSMS 中開啟檔案，然後按 F5 來執行指令碼。  
  
## <a name="next-step"></a>下一步  
 您可以精簡 Cube 權限來將存取權限制在資料格或維度資料。 如需詳細資訊，請參閱[授與維度資料的自訂存取權 &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md) 和[授與資料格資料的自訂存取權 &#40;Analysis Services&#41;](grant-custom-access-to-cell-data-analysis-services.md)。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 支援的驗證方法](../instances/authentication-methodologies-supported-by-analysis-services.md)   
 [授與資料採礦結構和模型的權限 &#40;Analysis Services&#41;](grant-permissions-on-data-mining-structures-and-models-analysis-services.md)   
 [授與資料來源物件的權限 &#40;Analysis Services&#41;](grant-permissions-on-a-data-source-object-analysis-services.md)  
  
  
