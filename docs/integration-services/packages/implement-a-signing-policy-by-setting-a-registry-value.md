---
title: "透過設定登錄值實作簽署原則 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "簽署原則 [Integration Services]"
ms.assetid: 64f6966f-2292-401f-acb1-2ccb5aee484a
caps.latest.revision: 27
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 27
---
# 透過設定登錄值實作簽署原則
  您可以使用選擇性登錄值來管理載入已簽署或未簽署之封裝的組織原則。 如果您使用這個登錄值，就必須在即將執行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝而且想要強制執行此原則的每部電腦上建立這個登錄值。 設定此登錄值之後，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 就會檢查或確認簽章，然後再載入封裝。  
  
 本主題中的這個程序描述如何將選擇性 **BlockedSignatureStates** DWORD 值加入至 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS 登錄機碼。 **BlockedSignatureStates** 中的資料值會決定在封裝具有不受信任的簽章、具有無效的簽章或未簽署時，是否應該封鎖它。 關於用來簽署封裝的簽章狀態，**BlockedSignatureStates** 登錄值會使用下列定義：  
  
-   「有效簽章」是指可以成功讀取的簽章。  
  
-   「無效簽章」是指簽章的解密總和檢查碼 (由私密金鑰加密之封裝程式碼的單向雜湊) 與載入 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝程序中導出的解密總和檢查碼不符。  
  
-   「信任簽章」是指使用由信任根憑證授權單位簽署的數位憑證所建立的簽章。 使用此設定時，簽署者不必出現在使用者的「受信任的發行者」清單中。  
  
-   「不受信任的簽章」是指無法確認為信任根憑證授權單位所發出的簽章，或不是目前的簽章。  
  
 下表列出 DWORD 資料的有效值及其相關聯的原則。  
  
|Value|描述|  
|-----------|-----------------|  
|0|沒有管理限制。|  
|1|封鎖無效的簽章。<br /><br /> 此設定不會封鎖未簽署的封裝。|  
|2|封鎖無效及不受信任的簽章。<br /><br /> 此設定不會封鎖未簽署的封裝，但是會封鎖自我產生的簽章。|  
|3|封鎖無效和不受信任的簽章以及未簽署的封裝<br /><br /> 此設定也會封鎖自我產生的簽章。|  
  
> [!NOTE]  
>  **BlockedSignatureStates** 的建議設定為 3。 此設定會提供最大程度的保護，以防範無效或不受信任的未簽署封裝或簽章。 但是，建議設定未必適合所有情況。 如需簽署數位資產的詳細資訊，請參閱 MSDN Library 中的 [Introduction to Code Signing](http://go.microsoft.com/fwlink/?LinkId=51414) (程式碼簽署簡介) 主題。  
  
### 實作封裝的簽署原則  
  
1.  在 **[開始]** 功能表上，按一下 **[執行]**。  
  
2.  在 [執行] 對話方塊中，輸入 **Regedit**，然後按一下 [確定]。  
  
3.  找出登錄機碼 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS。  
  
4.  以滑鼠右鍵按一下 [MSDTS]，指向 [新增]，然後按一下 [DWORD 值]。  
  
5.  將新值的名稱更新為 **BlockedSignatureStates**。  
  
6.  以滑鼠右鍵按一下 [BlockedSignatureStates]，然後按一下 [修改]。  
  
7.  在 [編輯 DWORD 值] 對話方塊中，輸入值 0、1、2 或 3。  
  
8.  按一下 **[確定]**。  
  
9. 在 **[檔案]** 功能表上按一下 **[結束]**。  
  
## 請參閱＜  
 [安全性概觀 &#40;Integration Services&#41;](../../integration-services/security/security-overview-integration-services.md)   
 [使用數位簽章來識別封裝的來源](../../integration-services/packages/identify-the-source-of-packages-with-digital-signatures.md)  
  
  