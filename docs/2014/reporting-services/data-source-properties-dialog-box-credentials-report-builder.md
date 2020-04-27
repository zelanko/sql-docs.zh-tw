---
title: 資料來源屬性對話方塊、認證（報表產生器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10017"
ms.assetid: 4531f09f-d653-4c05-a120-d7788838bc99
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5dd4d113c92e0a2d094aa02d49010a5dd477c6ba
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109448"
---
# <a name="data-source-properties-dialog-box-credentials-report-builder"></a>資料來源屬性對話方塊、認證 (報表產生器)
  選取 **[資料來源屬性]** 對話方塊上的 **[認證]** ，即可顯示和修改要連接到報表中內嵌資料來源的認證。 您所提供的認證會用來存取資料來源，以便預覽報表。 如需認證的詳細資訊，請參閱 [在報表產生器中指定認證](../../2014/reporting-services/specify-credentials-in-report-builder.md)。  
  
## <a name="options"></a>選項。  
 **使用 Windows 驗證 (整合式安全性)**  
 選取此選項即可使用 Windows 驗證。  
  
 **使用此使用者名稱和密碼**  
 選取此選項即可提供特定的使用者名稱和密碼。 若為內嵌資料來源：當您將報表伺服器專案發行至目標伺服器時，使用者名稱和密碼就會儲存成資料庫的預存認證。 如果您想要使用該使用者名稱和密碼當做 Windows 認證，就可以在目標伺服器上變更已發行共用資料來源的屬性。 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [線上叢書](https://go.microsoft.com/fwlink/?linkid=121312)》中 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 文件的[建立、刪除或修改共用資料來源 &#40;報表管理員&#41;](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md)。  
  
 **使用者名稱**  
 輸入使用者名稱以登入資料來源。  
  
 **密碼**  
 輸入密碼以登入資料來源。  
  
 **提示輸入認證**  
 選取此選項即可在執行報表時提示輸入認證。  
  
 **輸入提示字串**  
 輸入句子，以指示使用者提供資料來源的登入認證。  
  
 **無認證**  
 選取此選項就不會提供資料來源的認證。 只有在資料來源未接受認證，或是使用一些其他方式傳送認證時，這個選項才有用。  
  
 針對某些資料延伸模組，您就必須在報表伺服器上設定自動執行帳戶。  
  
 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [線上叢書](https://go.microsoft.com/fwlink/?linkid=121312)》之 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 文件中[從外部資料來源加入資料 &#40;SSRS&#41;](report-data/add-data-from-external-data-sources-ssrs.md) 和[設定自動執行帳戶 &#40;SSRS 組態管理員&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md) 中對應資料來源類型的主題。  
  
## <a name="see-also"></a>另請參閱  
 [對話方塊、窗格和嚮導的報表產生器說明](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [資料來源屬性對話方塊、一般 &#40;報表產生器&#41;](../../2014/reporting-services/data-source-properties-dialog-box-general-report-builder.md)   
 [加入及驗證資料連線或資料來源 &#40;報表產生器和 SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)   
 [將資料加入報表 &#40;報表產生器和 SSRS&#41;](report-data/report-datasets-ssrs.md)  
  
  
