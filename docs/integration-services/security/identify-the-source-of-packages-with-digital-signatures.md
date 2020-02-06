---
title: 使用數位簽章來識別套件的來源 | Microsoft Docs
ms.custom: security
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.digitalsigning.f1
helpviewer_keywords:
- signing packages [Integration Services]
- certificates [Integration Services]
- packages [Integration Services], security
- security [Integration Services], certificates
- signing policies [Integration Services]
ms.assetid: a433fbef-1853-4740-9d5e-8a32bc4ffbb2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fd8b17acb904ae0d33b06e85531e531792f1d60e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "71295698"
---
# <a name="identify-the-source-of-packages-with-digital-signatures"></a>使用數位簽章來識別封裝的來源

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  您可以使用數位憑證來簽署 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝，以便識別其來源。 當您已經使用數位憑證來簽署封裝之後，就可以讓 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 檢查數位簽章，然後再載入封裝。 若要讓 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 檢查簽章，您可以在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 或 **dtexec** 公用程式 (dtexec.exe) 中設定選項，或設定選擇性登錄值。  
  
## <a name="sign-a-package-with-a-digital-certificate"></a>使用數位憑證來簽署套件  
 您必須先取得或建立數位憑證，然後才能使用該憑證來簽署封裝。 當您擁有憑證之後，就可以使用這個憑證來簽署封裝。 如需如何取得憑證以及使用該憑證來簽署封裝的詳細資訊，請參閱 [使用數位憑證來簽署封裝](#cert)。  
  
## <a name="set-an-option-to-check-the-package-signature"></a>設定檢查套件簽章的選項  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 和 **dtexec** 公用程式都具有一個選項，可設定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 來檢查已簽署封裝的數位簽章。 您應該使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 或 **dtexec** 公用程式，取決於您想要檢查所有封裝或只檢查特定封裝：  
  
-   若要在設計階段載入封裝之前檢查所有封裝的數位簽章，請在  **中設定 [載入封裝時檢查數位簽章]** [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 選項。 這個選項是 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中所有封裝的全域設定。
  
-   若要檢查個別封裝的數位簽章，請在您使用 **dtexec** 公用程式來執行封裝時，指定 **/VerifyS[igned]** 選項。 如需詳細資訊，請參閱 [dtexec Utility](../../integration-services/packages/dtexec-utility.md)。  
  
## <a name="set-a-registry-value-to-check-package-signature"></a>設定檢查套件簽章的登錄值  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 也支援選擇性登錄值 **BlockedSignatureStates**，可讓您用來管理載入已簽署和未簽署封裝的組織原則。 如果封裝未經簽署或是具有無效或不受信任的簽章，此登錄值可以防止載入封裝。 如需如何設定此登錄值的詳細資訊，請參閱 [透過設定登錄值實作簽署原則](#registry)。  
  
> **注意：** 選擇性的 **BlockedSignatureStates** 登錄值所指定的設定，可以比 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中所設定或 **dtexec** 命令列上所設定的數位簽章選項更具限制性。 在此情況下，更具限制性的登錄設定會覆寫其他設定。  

## <a name="registry"></a> 透過設定登錄值實作簽署原則
  您可以使用選擇性登錄值來管理載入已簽署或未簽署之封裝的組織原則。 如果您使用這個登錄值，就必須在即將執行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝而且想要強制執行此原則的每部電腦上建立這個登錄值。 設定此登錄值之後， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 就會檢查或確認簽章，然後再載入封裝。  
  
 本主題中的這個程序描述如何將選擇性 **BlockedSignatureStates** DWORD 值加入至 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS 登錄機碼。 **BlockedSignatureStates** 中的資料值會決定在封裝具有不受信任的簽章、具有無效的簽章或未簽署時，是否應該封鎖它。 關於用來簽署封裝的簽章狀態， **BlockedSignatureStates** 登錄值會使用下列定義：  
  
-   「有效簽章」  是指可以成功讀取的簽章。  
  
-   「無效簽章」  是指簽章的解密總和檢查碼 (由私密金鑰加密之封裝程式碼的單向雜湊) 與載入 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝程序中導出的解密總和檢查碼不符。  
  
-   「信任簽章」  是指使用由信任根憑證授權單位簽署的數位憑證所建立的簽章。 使用此設定時，簽署者不必出現在使用者的「受信任的發行者」清單中。  
  
-   「不受信任的簽章」  是指無法確認為信任根憑證授權單位所發出的簽章，或不是目前的簽章。  
  
 下表列出 DWORD 資料的有效值及其相關聯的原則。  
  
|值|描述|  
|-----------|-----------------|  
|0|沒有管理限制。|  
|1|封鎖無效的簽章。<br /><br /> 此設定不會封鎖未簽署的封裝。|  
|2|封鎖無效及不受信任的簽章。<br /><br /> 此設定不會封鎖未簽署的封裝，但是會封鎖自我產生的簽章。|  
|3|封鎖無效和不受信任的簽章以及未簽署的封裝<br /><br /> 此設定也會封鎖自我產生的簽章。|  
  
> [!NOTE]  
>  **BlockedSignatureStates** 的建議設定為 3。 此設定會提供最大程度的保護，以防範無效或不受信任的未簽署封裝或簽章。 但是，建議設定未必適合所有情況。 如需簽署數位資產的詳細資訊，請參閱 MSDN Library 中的[Introduction to Code Signing](https://go.microsoft.com/fwlink/?LinkId=51414)(程式碼簽署簡介) 主題。  
  
### <a name="to-implement-a-signing-policy-for-packages"></a>實作封裝的簽署原則  
  
1.  在 **[開始]** 功能表上，按一下 **[執行]** 。  
  
2.  在 [執行] 對話方塊中，輸入 **Regedit**，然後按一下 [確定]  。  
  
3.  找出登錄機碼 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS。  
  
4.  以滑鼠右鍵按一下 [MSDTS]  ，指向 [新增]  ，然後按一下 [DWORD 值]  。  
  
5.  將新值的名稱更新為 **BlockedSignatureStates**。  
  
6.  以滑鼠右鍵按一下 [BlockedSignatureStates]  ，然後按一下 [修改]  。  
  
7.  在 [編輯 DWORD 值]  對話方塊中，輸入值 0、1、2 或 3。  
  
8.  按一下 [確定]  。  
  
9. 在 **[檔案]** 功能表上按一下 **[結束]** 。    

## <a name="cert"></a> 使用數位憑證來簽署封裝
  此主題描述如何使用數位憑證來簽署 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。 您可以使用數位簽章搭配其他設定，防止無效的封裝載入並執行。  
  
 簽署 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝之前，您必須執行下列工作：  
  
-   建立或取得要與憑證建立關聯的私密金鑰，然後將此私密金鑰儲存在本機電腦上。  
  
-   向信任的憑證授權單位取得用於程式碼簽署的憑證。 您可以使用下列其中一種方法來取得或建立憑證：  
  
    -   向發行憑證的公開商業憑證授權單位取得憑證。  
  
    -   從可以讓組織在內部發行憑證的憑證伺服器取得憑證。 您必須將用來簽署憑證的根憑證加入至 **[信任根憑證授權單位]** 存放區。 若要加入根憑證，您可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console (MMC) 的「憑證」嵌入式管理單元。 如需詳細資訊，請參閱 MSDN Library 中的＜[憑證服務](https://go.microsoft.com/fwlink/?LinkId=100755)＞(英文) 主題。  
  
    -   建立僅供測試用途的自訂憑證。 憑證建立工具 (Makecert.exe) 會產生供測試用途的 X.509 憑證。 如需詳細資訊，請參閱 MSDN Library 中的＜[憑證建立工具 (Makecert.exe)](https://go.microsoft.com/fwlink/?LinkId=100756)＞主題。  
  
     如需有關憑證的詳細資訊，請參閱「憑證」嵌入式管理單元的線上說明。 如需有關如何簽署數位資產的詳細資訊，請參閱 MSDN Library 中的[使用 Authenticode 簽署與檢查程式碼](https://go.microsoft.com/fwlink/?LinkId=78100)主題。  
  
-   確定憑證已經啟用程式碼簽署。 若要判斷憑證是否已啟用程式碼簽署，請在「憑證」嵌入式管理單元中檢閱憑證的屬性。  
  
-   將憑證儲存在個人存放區中。  
  
 當您已完成上述工作之後，就可以使用下列程序來簽署封裝。  
  
### <a name="to-sign-a-package"></a>若要簽署封裝  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含要簽署之封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  在 [ [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師] 的 **[SSIS]** 功能表上，按一下 **[數位簽章]** 。  
  
4.  在 **[數位簽章]** 對話方塊中，按一下 **[簽署]** 。  
  
5.  在 **[選取憑證]** 對話方塊中，選取憑證。  
  
6.  (選擇性) 按一下 [檢視憑證]  檢視憑證資訊。  
  
7.  按一下 **[確定]** 關閉 **[選取憑證]** 對話方塊。  
  
8.  按一下 **[確定]** 關閉 **[數位簽章]** 對話方塊。  
  
9. 若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
     雖然封裝已經簽署，但是您現在必須設定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ，以便檢查或確認數位簽章，然後再載入封裝。  

## <a name="signing_dialog"></a> 數位簽章對話方塊 UI 參考
  使用 **[數位簽章]** 對話方塊，即可使用數位簽章來簽署封裝，或是移除簽章。 在 **中，可從** [SSIS] **功能表的** [數位簽章] **選項來使用** [數位簽章] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]對話方塊。  
  
 如需詳細資訊，請參閱 [使用數位憑證來簽署封裝](#cert)。  
  
### <a name="options"></a>選項。  
 **簽署**  
 按一下即可開啟 [選取憑證]  對話方塊，並選取要使用的憑證。  
  
 **移除**  
 按一下即可移除數位簽章。  

## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 封裝](../../integration-services/integration-services-ssis-packages.md)   
 [安全性概觀 (Integration Services)](../../integration-services/security/security-overview-integration-services.md)  
  
  
