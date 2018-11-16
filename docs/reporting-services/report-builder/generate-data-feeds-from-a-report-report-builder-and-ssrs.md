---
title: 從報表產生資料摘要 (報表產生器及 SSRS) | Microsoft Docs
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: e68baae2-9f2a-4f13-9179-9ac7f29111c5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 84cef641a054fdf56c1fc8ca63dd87232d99a7fa
ms.sourcegitcommit: 9ece10c2970a4f0812647149d3de2c6b75713e14
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/16/2018
ms.locfileid: "51814251"
---
# <a name="generate-data-feeds-from-a-report-report-builder-and-ssrs"></a>從報表產生資料摘要 (報表產生器及 SSRS)

您可以從分頁報表產生符合 Atom 的資料摘要，然後在可取用資料摘要的應用程式 (例如 Power Pivot 或 Power BI) 中使用資料摘要。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Atom 轉譯延伸模組會產生 Atom 服務文件，其中會列出可從報表取得的資料摘要。 此文件至少會列出報表中每個資料區的一個資料摘要。 根據資料區的類型以及該資料區顯示的資料， [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 可能會產生來自某個資料區的多個資料摘要。  
  
 Atom 服務文件會針對每個資料摘要包含一個唯一的識別碼，而您可以在 URL 中使用該識別碼來檢視資料摘要的內容。  
  
 如需詳細資訊，請參閱 [從多個報表產生資料摘要 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md)中使用這項資料。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-generate-an-atom-service-document"></a>若要產生 Atom 服務文件  
  
1.  在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Web 入口網站上，導覽至您要產生其資料摘要的報表。  
  
2.  按一下報表。  
  
     報表隨即執行。  
  
3.  在工具列上，按一下**匯出至資料摘要**圖示。  
  
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
  
     `https://<server name>/ReportServer?%2f<ReportName>rs%3aCommand=Render&rs%3aFormat=ATOM&rc%3aDataFeed=<Identifier>`  
  
3.  按 ENTER 鍵。  
  
     此時會出現一個訊息，詢問您要開啟還是儲存包含資料摘要的 Atom 文件。  
  
4.  按一下 **[儲存]** ，將文件儲存至檔案系統，或按一下 **[開啟]** ，在儲存前檢視資料摘要。  
  
5.  瀏覽至要儲存文件的位置。  
  
6.  您可以選擇變更文件的名稱。  
  
    > [!NOTE]  
    >  依預設，文件名稱就是報表名稱。 如果 Atom 服務文件有多個摘要，預設全部都使用相同的名稱，也就是報表名稱。 若要區別這些摘要，請加以重新命名以使用有意義的名稱。  
  
7.  確認文件類型為 **[ATOM 檔]**，然後按一下 **[儲存]**。  
  
8.  或者，在瀏覽器或者文字編輯器或 XML 編輯器中開啟 .atom 檔。  

## <a name="next-steps"></a>後續步驟

[匯出報表](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](https://go.microsoft.com/fwlink/?LinkId=620231)
