---
title: 資料來源屬性對話方塊、 認證 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.datasourceproperties.credentials.f1
- "10100"
ms.assetid: 14c3eeb6-d37b-4fda-967b-43afcdb48119
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6423c2caca256a257f660eabb8ce5eaf2d81c55f
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59961514"
---
# <a name="data-source-properties-dialog-box-credentials"></a>資料來源屬性對話方塊、認證
  選取 **[資料來源屬性]** 對話方塊上的 **[認證]** ，來顯示和修改要連接到報表中資料來源的認證。 您所提供的認證會用來存取資料來源，並快取資料副本，以預覽報表。 如需如何快取預覽資料的詳細資訊，請參閱 [預覽報表](reports/previewing-reports.md)。 如需認證的詳細資訊，請參閱 [指定報表資料來源的認證及連接資訊](report-data/specify-credential-and-connection-information-for-report-data-sources.md)。  
  
## <a name="options"></a>選項。  
 **使用 Windows 驗證 （整合式安全性）**  
 選取此選項即可使用 Windows 驗證。  
  
 **使用此使用者名稱和密碼**  
 選取此選項即可提供特定的使用者名稱和密碼。 若為共用資料來源：當您將報表伺服器專案發行至目標伺服器時，使用者名稱和密碼就會儲存成資料庫的預存認證。 如果您想要使用該使用者名稱和密碼當做 Windows 認證，就可以在目標伺服器上編輯已發行共用資料來源的屬性。 如需詳細資訊，請參閱[建立、刪除或修改共用資料來源 &#40;報表管理員&#41;](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md)。  
  
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
  
## <a name="see-also"></a>另請參閱  
 [資料來源屬性對話方塊、 一般](../../2014/reporting-services/data-source-properties-dialog-box-general.md)   
 [指定報表資料來源的認證及連接資訊](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [報表產生器中的資料連接、資料來源及連接字串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)  
  
  
