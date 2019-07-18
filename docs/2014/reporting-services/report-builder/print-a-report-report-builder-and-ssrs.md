---
title: 列印報表 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: b96936c9-c387-41a9-8c19-6eb325769ffd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 737e8ebfd96d98bff9ed144db33189e141dc0cfd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107773"
---
# <a name="print-a-report-report-builder-and-ssrs"></a>列印報表 (報表產生器及 SSRS)
  將報表儲存至報表伺服器之後，您就可以從瀏覽器、報表管理員或任何用來檢視所匯出報表的應用程式，檢視及列印報表。 儲存報表之前，您可以在預覽報表時將它列印出來。  
  
 當您列印報表時，可以指定所要使用的紙張大小。 紙張大小會決定報表中的頁數及哪些報表資料適合每一頁的大小。 紙張大小只會影響以強制分頁轉譯器所轉譯的報表：PDF、影像和列印。 設定紙張大小對於其他轉譯器沒有任何作用。 如需詳細資訊，請參閱[轉譯行為 &#40;報表產生器及 SSRS&#41;](../report-design/rendering-behaviors-report-builder-and-ssrs.md)。  
  
 您可以從報表管理員中的報表檢視器工具列或報表產生器中的預覽，將報表匯出到手動分頁轉譯器，或是按一下 [列印] 按鈕來列印報表的複本。 您可能需要設定紙張大小或是其他版面設定屬性。 使用 **[報表屬性]** 對話方塊可變更版面設定屬性，包括紙張大小。  
  
 您可以在兩個不同位置中指定列印頁面邊界：設計模式和執行模式。  
  
-   **設計模式。** 當您在設計模式中設定頁面邊界時，這些設定就會在您儲存報表時儲存在報表定義中。  
  
-   **執行模式。** 當您在執行模式中設定頁面邊界時，這項資訊不會儲存在報表定義中。 下次列印報表時，除非您再次指定列印邊界，否則將會從報表定義中取得設定。  
  
    > [!NOTE]  
    >  在設計或執行模式中，不會顯示列印邊界。 設計介面區域與報表的列印區域之間沒有任何關聯性。 若要查看列印邊界，請在執行模式中，於 [功能區] 的 **[執行]** 索引標籤上，按一下 [整頁模式]。  
  
 如需報表分頁的詳細資訊，請參閱 [Reporting Services 中的分頁 &#40;報表產生器及 SSRS&#41;](../report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-print-a-report-in-report-builder"></a>在報表產生器中列印報表  
  
1.  開啟報表。  
  
2.  在 [主資料夾] 索引標籤上，按一下 **[執行]** 。  
  
3.  (選擇性) 按一下 [整頁模式]  查看報表列印時的外觀。  
  
4.  (選擇性) 按一下 [版面設定]  設定紙張、方向與邊界。  
  
    > [!NOTE]  
    >  這些設定的預設值來自 [設計] 檢視中所設定的報表屬性。 您在 **[版面設定]** 對話方塊中設定的值只會用於此工作階段。 當您關閉這份報表並重新開啟時，它就會再次具有預設值。  
  
5.  按一下 **[列印]** 。  
  
6.  在 **[列印]** 對話方塊中，選取印表機並指定其他列印選項。  
  
### <a name="to-print-a-report-from-a-web-browser-application"></a>若要從網頁瀏覽器應用程式列印報表  
  
1.  啟動[報表管理員 &#40;SSRS 原生模式&#41;](../report-manager-ssrs-native-mode.md)。  
  
2.  在報表管理員中，導覽到您要列印的報表。 開啟報表。  
  
3.  在報表頂端的工具列上，按一下 **[列印]** 。  
  
    > [!NOTE]  
    >  您第一次列印 HTML 報表時，報表伺服器會提示您安裝用於列印的 ActiveX 控制項。 您必須安裝並設定控制項才能列印。  
  
4.  在 **[列印]** 對話方塊中，選取一個印表機，然後按一下 **[列印]** 。  
  
### <a name="to-print-a-report-from-other-applications"></a>若要從其他應用程式列印報表  
  
1.  在報表管理員中，導覽到您要列印的報表。 開啟報表。  
  
2.  在報表頂端的工具列上，選取一種轉譯格式，然後按一下 **[匯出]** 。 報表會在對應至轉譯格式的檢視器應用程式中開啟。  
  
     例如，如果您選取 PDF，則報表會在 Adobe Acrobat Reader 中開啟。  
  
3.  在該程式的 **[檔案]** 功能表上，按一下 **[列印]** 。  
  
### <a name="to-change-paper-size"></a>變更紙張大小  
  
1.  以滑鼠右鍵按一下報表主體的外面，然後按一下 [報表屬性]  。  
  
2.  在 **[版面設定]** 中，從 **[紙張大小]** 清單選取一個值。 每個選項都會填入 **[寬度]** 和 **[高度]** 屬性。 您也可以指定自訂大小，其方式是在 **[寬度]** 和 **[高度]** 方塊內輸入數值。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  大小值的預設單位視使用者的地區設定而定。 若要指定不同的單位，請在數值後面輸入一個實體單位指示項，例如 cm、mm、pt 或 pc。  
  
### <a name="to-set-page-margins-in-design-mode"></a>在設計模式中設定頁面邊界  
  
-   以滑鼠右鍵按一下設計介面周圍的藍色區域，按一下 [報表屬性]  ，然後按一下 [版面設定]  頁面。  
  
### <a name="to-set-page-margins-in-run-mode"></a>若要在執行模式中設定頁面邊界  
  
-   按一下 **[執行]** 索引標籤上的 **[版面設定]** 。  
  
## <a name="see-also"></a>另請參閱  
 [列印報表 &#40;報表產生器及 SSRS&#41;](print-reports-report-builder-and-ssrs.md)   
 [匯出報表&#40;報表產生器及 SSRS&#41;](export-reports-report-builder-and-ssrs.md)   
 [報表屬性對話方塊、版面設定 &#40;報表產生器&#41;](../report-properties-dialog-box-page-setup-report-builder.md)   
 [報表設計檢視 &#40;報表產生器&#41;](report-design-view-report-builder.md)  
  
  
