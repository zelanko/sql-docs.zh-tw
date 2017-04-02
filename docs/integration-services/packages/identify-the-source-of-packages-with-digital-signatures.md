---
title: "使用數位簽章來識別封裝的來源 | Microsoft Docs"
ms.custom: ""
ms.date: "08/24/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "簽署封裝 [Integration Services]"
  - "憑證 [Integration Services]"
  - "封裝 [Integration Services], 安全性"
  - "安全性 [Integration Services], 憑證"
  - "簽署原則 [Integration Services]"
ms.assetid: a433fbef-1853-4740-9d5e-8a32bc4ffbb2
caps.latest.revision: 46
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 46
---
# 使用數位簽章來識別封裝的來源
  您可以使用數位憑證來簽署 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝，以便識別其來源。 當您已經使用數位憑證來簽署封裝之後，就可以讓 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 檢查數位簽章，然後再載入封裝。 若要讓 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 檢查簽章，您可以在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 或 **dtexec** 公用程式 (dtexec.exe) 中設定選項，或設定選擇性登錄值。  
  
## 使用數位憑證來簽署套件  
 您必須先取得或建立數位憑證，然後才能使用該憑證來簽署封裝。 當您擁有憑證之後，就可以使用這個憑證來簽署封裝。 如需如何取得憑證以及使用該憑證來簽署封裝的詳細資訊，請參閱[使用數位憑證來簽署封裝](../../integration-services/packages/sign-a-package-by-using-a-digital-certificate.md)。  
  
## 設定檢查套件簽章的選項  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 和 **dtexec** 公用程式都具有一個選項，可設定 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 來檢查已簽署封裝的數位簽章。 您應該使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 或 **dtexec** 公用程式，取決於您想要檢查所有封裝或只檢查特定封裝：  
  
-   若要在設計階段載入封裝之前檢查所有封裝的數位簽章，請在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中設定 [載入封裝時檢查數位簽章] 選項。 這個選項是 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中所有封裝的全域設定。
  
-   若要檢查個別封裝的數位簽章，請在您使用 **dtexec** 公用程式來執行封裝時，指定 **/VerifyS[igned]** 選項。 如需詳細資訊，請參閱 [dtexec Utility](../../integration-services/packages/dtexec-utility.md)。  
  
## 設定檢查套件簽章的登錄值  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 也支援選擇性登錄值 **BlockedSignatureStates**，可讓您用來管理載入已簽署和未簽署封裝的組織原則。 如果封裝未經簽署或是具有無效或不受信任的簽章，此登錄值可以防止載入封裝。 如需如何設定此登錄值的詳細資訊，請參閱[透過設定登錄值實作簽署原則](../../integration-services/packages/implement-a-signing-policy-by-setting-a-registry-value.md)。  
  
> **注意：**選擇性的 **BlockedSignatureStates** 登錄值所指定的設定，可以比 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中所設定或 **dtexec** 命令列上所設定的數位簽章選項更具限制性。 在此情況下，更具限制性的登錄設定會覆寫其他設定。  
  
## 另請參閱  
 [Integration Services &#40;SSIS&#41; 封裝](../../integration-services/integration-services-ssis-packages.md)   
 [安全性概觀 &#40;Integration Services&#41;](../../integration-services/security/security-overview-integration-services.md)  
  
  