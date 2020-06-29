---
title: 使用數位憑證來簽署封裝 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- digital signatures [Integration Services]
- signing packages [Integration Services]
- signatures [Integration Services]
ms.assetid: 182b115e-0fe2-4717-8dff-183f9eb6e397
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f0cf5ff8cf0192968c94300977f38d3dd05984a1
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85421485"
---
# <a name="sign-a-package-by-using-a-digital-certificate"></a>使用數位憑證來簽署封裝
  此主題描述如何使用數位憑證來簽署 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝。 您可以使用數位簽章搭配其他設定，防止無效的封裝載入並執行。  
  
 簽署 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝之前，您必須執行下列工作：  
  
-   建立或取得要與憑證建立關聯的私密金鑰，然後將此私密金鑰儲存在本機電腦上。  
  
-   向信任的憑證授權單位取得用於程式碼簽署的憑證。 您可以使用下列其中一種方法來取得或建立憑證：  
  
    -   向發行憑證的公開商業憑證授權單位取得憑證。  
  
    -   從可以讓組織在內部發行憑證的憑證伺服器取得憑證。 您必須將用來簽署憑證的根憑證加入至 **[信任根憑證授權單位]** 存放區。 若要加入根憑證，您可以使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console (MMC) 的「憑證」嵌入式管理單元。 如需詳細資訊，請參閱 MSDN Library 中的＜[憑證服務](https://go.microsoft.com/fwlink/?LinkId=100755)＞(英文) 主題。  
  
    -   建立僅供測試用途的自訂憑證。 憑證建立工具 (Makecert.exe) 會產生供測試用途的 X.509 憑證。 如需詳細資訊，請參閱 MSDN Library 中的＜[憑證建立工具 (Makecert.exe)](https://go.microsoft.com/fwlink/?LinkId=100756)＞主題。  
  
     如需有關憑證的詳細資訊，請參閱「憑證」嵌入式管理單元的線上說明。 如需有關如何簽署數位資產的詳細資訊，請參閱 MSDN Library 中的[使用 Authenticode 簽署與檢查程式碼](https://go.microsoft.com/fwlink/?LinkId=78100)主題。  
  
-   確定憑證已經啟用程式碼簽署。 若要判斷憑證是否已啟用程式碼簽署，請在「憑證」嵌入式管理單元中檢閱憑證的屬性。  
  
-   將憑證儲存在個人存放區中。  
  
 當您已完成上述工作之後，就可以使用下列程序來簽署封裝。  
  
### <a name="to-sign-a-package"></a>若要簽署封裝  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含要簽署之封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  在 [ [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師] 的 **[SSIS]** 功能表上，按一下 **[數位簽章]** 。  
  
4.  在 **[數位簽章]** 對話方塊中，按一下 **[簽署]** 。  
  
5.  在 **[選取憑證]** 對話方塊中，選取憑證。  
  
6.  (選擇性) 按一下 [檢視憑證]  檢視憑證資訊。  
  
7.  按一下 **[確定]** 關閉 **[選取憑證]** 對話方塊。  
  
8.  按一下 **[確定]** 關閉 **[數位簽章]** 對話方塊。  
  
9. 若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
     雖然封裝已經簽署，但是您現在必須設定 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ，以便檢查或確認數位簽章，然後再載入封裝。 如需詳細資訊，請參閱 [Identify the Source of Packages with Digital Signatures](security/identify-the-source-of-packages-with-digital-signatures.md)(使用數位簽章識別封裝來源)。  
  
## <a name="see-also"></a>另請參閱  
 [安全性概觀 (Integration Services)](security/security-overview-integration-services.md)  
  
  
