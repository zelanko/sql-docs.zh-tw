---
title: 報表、報表組件和報表定義 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- report definitions
- reports
ms.assetid: 2d746550-f8cc-4e97-8a06-d0f03cffc18d
caps.latest.revision: 23
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 55004b30ac7f462b677875f6f8b872ccebf25be8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36022588"
---
# <a name="reports-report-parts-and-report-definitions-report-builder-and-ssrs"></a>報表、報表組件和報表定義 (報表產生器及 SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 您可以使用各種詞彙來描述不同狀態，包括初始定義、 已發行的報表，以及檢視的報表，顯示給使用者的報表。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-definition-rdl-files"></a>報表定義 (.rdl) 檔案  
 報表定義是您在報表產生器或報表設計師中建立的檔案。 它提供資料來源連接、用於擷取資料之查詢、運算式、參數、影像、文字方塊、資料表，以及您可能包含在報表中之其他任何設計階段元素的完整描述。 雖然報表定義可以很複雜，不過它至少會指定查詢和其他報表內容、報表屬性，以及報表配置。  
  
 報表定義會在執行階段轉譯成已處理的報表。 這時候，系統會從資料來源中擷取資料，並且根據報表定義中的指示格式化這項資料。 您可以直接從電腦執行報表定義並儲存在本機，也可以將它發行到報表伺服器，讓其他人執行。  
  
 報表定義是以符合 XML 文法 (稱為報表定義語言 (RDL)) 的 XML 所撰寫。 RDL 描述 XML 元素，包含報表可能出現的所有可能變化。  
  
## <a name="client-report-definition-rdlc-files"></a>用戶端報表定義 (.rdlc) 檔案  
 Visual Studio 報表設計師會產生可搭配 ReportViewer 控制項使用的用戶端報表定義 (.rdlc) 檔案。 這些 .rdlc 檔案可轉換成 .rdl 檔案，以搭配 Reporting Services 報表設計師使用。  
  
## <a name="report-part-rsc-files"></a>報表組件檔 (.rsc)  
 報表組件定義是報表定義檔的 XML 片段。 您可藉由建立報表定義，然後選取報表中的報表項目個別發行為報表組件，藉此建立報表組件。 報表組件包括資料區、矩形與其包含的項目，以及影像。 您可以將報表組件與其相依的資料集和共用資料來源參考一併儲存，以便於其他報表中重複使用。  
  
 [!INCLUDE[ssRBrptparts](../../includes/ssrbrptparts-md.md)]  
  
## <a name="published-reports"></a>已發行的報表  
 建立 .rdl 檔案之後，您就可以將它儲存在本機，也可以將它儲存至報表伺服器上的個人資料夾 (例如 [我的報表] 資料夾)。 報表可供其他人查看時，可以將它從報表產生器儲存到報表伺服器上的公用資料夾，然後透過報表管理員上載或是從報表設計師部署報表專案方案的方式來發行該報表。 已發行的報表是儲存在報表伺服器資料庫中，並在報表伺服器或 SharePoint 網站上管理的項目。  
  
 已發行的報表會透過使用 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 以角色為基礎之安全性模型的角色指派來維護其安全。 您可以透過 URL、SharePoint Web 組件或報表管理員存取已發行的報表，也可以在報表產生器中導覽並開啟它們。  
  
### <a name="report-snapshots"></a>報表快照集  
 您也可以將報表當做快照集來發行 (其中包含報表一開始執行時的配置資訊和資料)。 報表快照集不會以特定轉譯格式儲存。 而是只有在使用者或應用程式要求它時，報表快照集才以最後的檢視格式轉譯 (例如 HTML)。 如需詳細資訊，請參閱[在報表管理員中尋找及檢視報表 &#40;報表產生器及 SSRS&#41;](../report-builder/finding-and-viewing-reports-in-the-web-portal-report-builder-and-ssrs.md)。  
  
## <a name="rendered-reports"></a>已轉譯的報表  
 已轉譯的報表是一種完全處理的報表，其中包含採用適合檢視之格式 (例如 HTML) 的資料與配置資訊。 報表要等到轉譯成輸出格式後，才能夠檢視。 您可以執行下列任一種動作來轉譯報表：  
  
-   在報表產生器或報表設計師中建立或開啟報表並且執行它。  
  
-   在報表管理員中尋找並執行報表。  
  
-   在與 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 報表伺服器整合的 SharePoint 網站上尋找並執行報表。  
  
-   訂閱報表，訂閱的報表會以您指定的輸出格式傳遞到電子郵件收件匣或檔案共用。  
  
 訂閱報表，訂閱的報表會以您指定的輸出格式傳遞到電子郵件收件匣或檔案共用。報表的預設轉譯格式為 HTML 4.0。 除了 HTML 以外，報表還可以使用許多輸出格式轉譯，包括 Excel、Word、XML、PDF、TIFF 與 CSV。 如同已發行的報表一樣，已轉譯的報表也無法編輯或回存到報表伺服器。 如需詳細資訊，請參閱[匯出報表&#40;報表產生器及 SSRS&#41;](../report-builder/export-reports-report-builder-and-ssrs.md)。  
  
## <a name="see-also"></a>另請參閱  
 [報表撰寫概念&#40;報表產生器和 SSRS&#41;](report-authoring-concepts-report-builder-and-ssrs.md)   
 [SQL Server 2014 中的報表產生器](../report-builder/report-builder-in-sql-server-2016.md)   
 [安裝、 解除安裝，以及報表產生器支援](../install-uninstall-and-report-builder-support.md)   
 [尋找、檢視和管理報表 &#40;報表產生器及 SSRS &#41;](../report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [將報表匯出&#40;報表產生器和 SSRS&#41;](../report-builder/export-reports-report-builder-and-ssrs.md)  
  
  