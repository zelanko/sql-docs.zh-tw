---
title: 資料來源屬性對話方塊、 一般 （報表產生器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10018"
ms.assetid: b956f43a-8426-4679-acc1-00f405d5ff5b
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 977a7dcb943b3479dd5649cfcf842aefcf469e90
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56285716"
---
# <a name="data-source-properties-dialog-box-general-report-builder"></a>資料來源屬性對話方塊、一般 (報表產生器)
  選取 **[資料來源屬性]** 對話方塊上的 **[一般]** ，即可從報表伺服器中選取共用資料來源，或針對報表中內嵌的資料來源建立或修改連接資訊。  
  
 用來連接資料來源的認證類型是在資料來源屬性中指定。 當您開啟報表伺服器中的報表時，在資料來源屬性中指定的執行階段認證可能不適用於設計階段工作，例如建立查詢和預覽報表。 例如，資料來源可能會使用 Windows 認證 (而非您的認證)，或您不知道的使用者名稱和密碼。  
  
 當報表產生器無法使用資料來源屬性中提供的認證連線至資料來源時，會開啟 **[輸入資料來源認證]** 對話方塊。 這通常是在以下情況時發生：  
  
-   資料來源設定為提示認證。  
  
-   資料來源設定為使用預存認證。  為了盡量降低潛在的安全性威脅，報表產生器已設計成不會擷取伺服器上儲存的認證。  
  
 您可以使用 **[輸入資料來源認證]** 對話方塊來變更報表產生器在設計階段所使用的認證，以當做目前的 Windows 使用者連線至資料來源或提供使用者名稱和密碼。 如果您提供使用者名稱和密碼，則可以指出是否將使用者名稱和密碼當做 Windows 認證使用。  
  
> [!NOTE]  
>  雖然查詢設計工具可讓您指定用於設計階段認證的其他認證類型，但是報表預覽僅能讓您針對資料來源中指定的現有認證選項，輸入使用者名稱和密碼。  
  
 當您按一下 **[測試連接]** 時，系統會使用資料來源屬性認證頁面中所指定的認證測試資料來源的連接。 您可以測試內嵌和共用資料來源的連接。  
  
 如果指定的認證不完整 (例如，需要密碼)，報表產生器會在需要連接資料來源時，再次提示您輸入執行階段認證。 系統會儲存設計階段認證，因此不會再次提示。  
  
## <a name="options"></a>選項。  
 **名稱**  
 輸入資料來源的名稱。 資料來源名稱在報表內必須是唯一的。 根據預設，系統會將一般名稱 (例如，DataSource1 或 DataSource2) 指派給資料來源。  
  
 **使用共用的連線**  
 選取此選項，即可瀏覽至已經發行到報表伺服器的共用資料來源。  
  
 在您從報表伺服器中選取資料來源之後，報表產生器就會維持這個報表伺服器的連接。  
  
 **使用我的報表中內嵌的連接**  
 選取此選項，即可建立僅供這份報表使用的資料來源。  
  
 **型別**  
 選取資料處理延伸模組。 此清單會顯示所有已註冊的延伸模組。  
  
 **連接字串**  
 輸入資料來源的連接字串。 按一下 **[建立]** ，即可使用 **[連接屬性]** 對話方塊來建立連接字串。 請按一下 [運算式] (*fx*) 按鈕來編輯運算式。  
  
 **處理查詢時，使用單一交易**  
 選取此選項，指出使用此資料來源的資料集會在單一交易中針對資料庫執行。 若要包含使用相同資料來源之子報表的交易，請選取子報表，然後在 [屬性] 窗格中，將 **[MergeTransactions]** 設定為 **[True]**。  
  
 **測試連接**  
 按一下以使用指定的認證確認資料來源連接能夠運作。 如果無法建立連接，您需要確認認證和伺服器可用性。 可以測試內嵌和共用資料來源的資料來源連接。  
  
## <a name="see-also"></a>另請參閱  
 [將資料加入至報表&#40;報表產生器及 SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [加入及驗證資料連接或資料來源&#40;報表產生器及 SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)   
 [報表產生器中的資料連接、資料來源及連接字串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)   
 [資料來源屬性對話方塊、 認證&#40;報表產生器&#41;](../../2014/reporting-services/data-source-properties-dialog-box-credentials-report-builder.md)   
 [對話方塊、窗格和精靈的報表產生器說明](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)  
  
  
