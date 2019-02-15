---
title: 將報表匯出為其他檔案類型 （報表產生器及 SSRS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: b577568b-ecbd-44c3-be88-31dab6fc38a2
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 009cce23aff5d3b3755b4eb8086bd1560a5be487
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56289090"
---
# <a name="export-a-report-as-another-file-type-report-builder-and-ssrs"></a>將報表匯出為其他檔案類型 (報表產生器及 SSRS)
  當您在報表產生器或報表設計師中預覽報表時，可以將報表轉譯為其他檔案格式，例如 CSV、影像、PDF、 [!INCLUDE[ofprword](../includes/ofprword-md.md)]或 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)]，或者，當您在報表伺服器上檢視報表時，也可以轉譯報表。 如果您想要將報表立即儲存為其他檔案類型，而不要將報表發行到報表伺服器，或者您想要查看以特定格式將報表設計傳遞給報表讀者時的外觀，使用特定格式來轉譯報表會相當有用。 當您設定訂閱或透過電子郵件傳遞報表時，或者，如果您想要儲存報表伺服器上提供的報表時，在報表伺服器上轉譯報表很有用。 如需詳細資訊，請參閱[訂閱與傳遞 &#40;Reporting Services&#41;](subscriptions/subscriptions-and-delivery-reporting-services.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
### <a name="to-export-a-report-as-another-file-type-in-report-builder"></a>若要在報表產生器中將報表匯出為其他檔案類型  
  
1.  預覽報表。  
  
2.  在功能區上按一下 **[匯出]**。  
  
3.  選取要使用的格式。  
  
     **[另存新檔]** 對話方塊隨即開啟。 依預設，檔案名稱就是您匯出之報表的名稱。 您可以選擇變更檔案名稱。  
  
4.  導覽至您儲存匯出之報表的位置，然後將它開啟。  
  
> [!NOTE]  
>  如果因為您沒有與此檔案類型相關聯的程式而無法以您所選擇的格式開啟報表，系統將會提示您儲存匯出的報表，或在線上尋找一個程式來開啟該報表。  
  
### <a name="to-export-a-report-as-another-file-type-in-report-manager"></a>若要在報表管理員中將報表匯出為其他檔案類型  
  
1.  從「報表管理員」的 **[首頁]** 頁面上，導覽至您要匯出的報表。  
  
2.  按一下報表。  
  
     系統便會產生報表。  
  
3.  在 [報表檢視器] 工具列上，按一下 **[選取格式]** 下拉箭頭。  
  
4.  選取要使用的格式。  
  
5.  按一下 **[匯出]**。  
  
     此時會出現一個訊息，詢問您要開啟還是儲存檔案。  
  
6.  若要以選取的匯出格式檢視報表，按一下 **[開啟]**。  
  
     \-或-  
  
     若要以選取的匯出格式立即儲存報表，按一下 **[儲存]**。  
  
     使用與您選擇之格式相關聯的應用程式，顯示或儲存報表。 如果您按一下 **[儲存]**，系統會提示您儲存報表的位置。  
  
     **注意** ：如果因為您沒有與此檔案類型相關聯的程式而無法以您所選擇的格式開啟報表，系統將會提示您儲存匯出的報表，或在線上尋找一個程式來開啟該報表。  
  
### <a name="to-export-a-report-as-another-file-type-in-a-sharepoint-library"></a>若要在 SharePoint 文件庫中將報表匯出為其他檔案類型  
  
1.  預覽報表。  
  
2.  在工具列上，按一下 **[動作]**，指向 **[匯出]**，然後選取您要使用的格式。  
  
     隨即開啟 **[檔案下載]** 對話方塊。  
  
3.  若要以選取的匯出格式檢視報表，按一下 **[開啟]**。  
  
     \-或-  
  
     若要以選取的匯出格式立即儲存報表，按一下 **[儲存]**。  
  
     使用與您選擇之格式相關聯的應用程式，顯示或儲存報表。 如果您按一下 **[儲存]**，系統會提示您儲存報表的位置。  
  
     您可以選擇變更匯出之報表的檔案名稱。  
  
     **注意** ：如果因為您沒有與此檔案類型相關聯的程式而無法以您所選擇的格式開啟報表，系統將會提示您儲存匯出的報表，或在線上尋找一個程式來開啟該報表。  
  
## <a name="see-also"></a>另請參閱  
 [匯出報表&#40;報表產生器及 SSRS&#41;](report-builder/export-reports-report-builder-and-ssrs.md)   
 [Reporting Services 中的分頁 &#40;報表產生器及 SSRS&#41;](report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [不同報表轉譯延伸模組的互動式功能&#40;報表產生器及 SSRS&#41;](report-builder/interactive-functionality-different-report-rendering-extensions.md)  
  
  
