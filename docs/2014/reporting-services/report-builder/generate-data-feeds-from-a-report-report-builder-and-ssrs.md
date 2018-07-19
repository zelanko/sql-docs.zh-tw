---
title: 從報表產生資料摘要 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e68baae2-9f2a-4f13-9179-9ac7f29111c5
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 4ee1402202e08ab4ba718238b454f5eb4e548118
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37210828"
---
# <a name="generate-data-feeds-from-a-report-report-builder-and-ssrs"></a>從報表產生資料摘要 (報表產生器及 SSRS)
  您可以從報表產生符合 Atom 資料摘要，然後這類應用程式中，使用資料摘要[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]用戶端可以取用資料摘要。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Atom 轉譯延伸模組會產生 Atom 服務文件，其中會列出可從報表取得的資料摘要。 此文件至少會列出報表中每個資料區的一個資料摘要。 根據資料區的類型以及該資料區顯示的資料， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 可能會產生來自某個資料區的多個資料摘要。  
  
 Atom 服務文件會針對每個資料摘要包含一個唯一的識別碼，而您可以在 URL 中使用該識別碼來檢視資料摘要的內容。  
  
 如需詳細資訊，請參閱[從多個報表產生資料摘要 &#40;報表產生器及 SSRS&#41;](generating-data-feeds-from-reports-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-generate-an-atom-service-document"></a>若要產生 Atom 服務文件  
  
1.  從報表管理員的 **[主資料夾]** 頁面上，導覽至您要從其中產生資料摘要的報表。  
  
2.  按一下報表。  
  
     報表隨即執行。  
  
3.  在工具列上，按一下 [匯出至資料摘要] 圖示。  
  
     此時會出現一個訊息，詢問您要開啟還是儲存包含資料摘要的 Atom 文件。  
  
4.  按一下 **[儲存]** ，將文件儲存至檔案系統，或按一下 **[開啟]** ，在儲存前檢視文件內容。 **依預設，文件會在瀏覽器中開啟。**  
  
5.  瀏覽至要儲存文件的位置。  
  
6.  您可以選擇變更文件的名稱。  
  
    > [!NOTE]  
    >  依預設，文件名稱就是報表名稱。  
  
7.  確認文件類型為 **[ATOMSVC 檔]**，然後按一下 **[儲存]**。  
  
8.  或者，在瀏覽器或者文字或 XML 編輯器中開啟 .atomsvc 檔。  
  
### <a name="to-view-an-atom-compliant-data-feed"></a>若要檢視符合 Atom 的資料摘要  
  
1.  如果尚未開啟 Atom 服務文件，請找出該文件並在瀏覽器 (例如 Internet Explorer) 中開啟。  
  
2.  將您要檢視的資料摘要 URL 從 Atom 服務文件複製到瀏覽器。  
  
     URL 的格式為：  
  
 `http://<server name>/ReportServer?%2f<ReportName>rs%3aCommand=Render&rs%3aFormat=ATOM&rc%3aDataFeed=<Identifier>`  
  
1.  按 ENTER 鍵。  
  
     此時會出現一個訊息，詢問您要開啟還是儲存包含資料摘要的 Atom 文件。  
  
2.  按一下 **[儲存]** ，將文件儲存至檔案系統，或按一下 **[開啟]** ，在儲存前檢視資料摘要。  
  
3.  瀏覽至要儲存文件的位置。  
  
4.  您可以選擇變更文件的名稱。  
  
    > [!NOTE]  
    >  依預設，文件名稱就是報表名稱。 如果 Atom 服務文件有多個摘要，預設全部都使用相同的名稱，也就是報表名稱。 若要區別這些摘要，請加以重新命名以使用有意義的名稱。  
  
5.  確認文件類型為 **[ATOM 檔]**，然後按一下 **[儲存]**。  
  
6.  或者，在瀏覽器或者文字編輯器或 XML 編輯器中開啟 .atom 檔。  
  
## <a name="see-also"></a>另請參閱  
 [匯出報表&#40;報表產生器及 SSRS&#41;](export-reports-report-builder-and-ssrs.md)  
  
  
