---
title: 使用數位簽章來識別套件的來源 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- signing packages [Integration Services]
- certificates [Integration Services]
- packages [Integration Services], security
- security [Integration Services], certificates
- signing policies [Integration Services]
ms.assetid: a433fbef-1853-4740-9d5e-8a32bc4ffbb2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 90c0e2e3db13ba4b228b70ccfffddbc2ff221774
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85422115"
---
# <a name="identify-the-source-of-packages-with-digital-signatures"></a>使用數位簽章來識別封裝的來源
  您可以使用數位憑證來簽署 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝，以便識別其來源。 當您已經使用數位憑證來簽署封裝之後，就可以讓 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 檢查數位簽章，然後再載入封裝。 若要讓 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 檢查簽章，您可以在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 或 **dtexec** 公用程式 (dtexec.exe) 中設定選項，或設定選擇性登錄值。  
  
## <a name="signing-a-package-with-a-digital-certificate"></a>使用數位憑證來簽署封裝  
 您必須先取得或建立數位憑證，然後才能使用該憑證來簽署封裝。 當您擁有憑證之後，就可以使用這個憑證來簽署封裝。 如需如何取得憑證以及使用該憑證來簽署封裝的詳細資訊，請參閱 [使用數位憑證來簽署封裝](../sign-a-package-by-using-a-digital-certificate.md)。  
  
## <a name="setting-an-option-to-check-the-package-signature"></a>設定檢查封裝簽章的選項  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 和 **dtexec** 公用程式都具有一個選項，可設定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 來檢查已簽署封裝的數位簽章。 您應該使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 或 **dtexec** 公用程式，取決於您想要檢查所有封裝或只檢查特定封裝：  
  
-   若要在設計階段載入封裝之前檢查所有封裝的數位簽章，請在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中設定 [載入封裝時檢查數位簽章]  選項。 這個選項是 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中所有封裝的全域設定。 如需相關資訊，請參閱 [General Page](../general-page-of-integration-services-designers-options.md)。  
  
-   若要檢查個別封裝的數位簽章，請在 `/VerifyS[igned]` 使用**dtexec**公用程式來執行封裝時，指定選項。 如需詳細資訊，請參閱 [dtexec Utility](../packages/dtexec-utility.md)。  
  
## <a name="setting-a-registry-value-to-check-the-package-signature"></a>設定檢查封裝簽章的登錄值  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 也支援選擇性登錄值 **BlockedSignatureStates**，可讓您用來管理載入已簽署和未簽署封裝的組織原則。 如果封裝未經簽署或是具有無效或不受信任的簽章，此登錄值可以防止載入封裝。 如需如何設定此登錄值的詳細資訊，請參閱 [透過設定登錄值實作簽署原則](../implement-a-signing-policy-by-setting-a-registry-value.md)。  
  
> [!NOTE]  
>  選擇性的 **BlockedSignatureStates** 登錄值所指定的設定，可以比 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中所設定或 **dtexec** 命令列上所設定的數位簽章選項更具限制性。 在此情況下，更具限制性的登錄設定會覆寫其他設定。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 封裝](../integration-services-ssis-packages.md)   
 [安全性概觀 (Integration Services)](security-overview-integration-services.md)  
  
  
