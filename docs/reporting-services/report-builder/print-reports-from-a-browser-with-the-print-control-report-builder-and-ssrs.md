---
title: "從列印控制項 （報表產生器及 SSRS） 與瀏覽器列印報表 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 10054250-d915-4bcb-8a1d-26837db4e932
caps.latest.revision: 13
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3674bb697d86ac79906aa4ee5172ad24030a22fc
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs"></a>使用列印控制項從瀏覽器列印報表 (報表產生器及 SSRS)
  雖然瀏覽器是最常用來檢視報表的用戶端應用程式，但瀏覽器的列印功能在列印報表時並不理想。 瀏覽器的列印功能是為了列印網頁而設計的。 通常，您從瀏覽器列印的頁面會包括網頁上的所有視覺化元素，以及識別網頁或網站的頁首和頁尾資訊。 從瀏覽器列印時會列印現行視窗的內容。 若為多頁報表．瀏覽器最多只會列印第一頁，如果報表頁面延伸到列印頁面範圍之外，則列印出來的可能更少。  
  
 若要改善您在瀏覽器中檢視之報表的列印品質並列印多個頁面，您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中提供的用戶端列印功能。 用戶端列印功能提供標準的 **[列印]** 對話方塊，可以用來選取印表機、指定頁面和邊界，以及在列印之前先預覽報表。 用戶端列印功能就是要用來代替瀏覽器 **[檔案]** 功能表上的 **[列印]** 命令。 使用用戶端列印功能時，報表會像原來設計那樣列印出來，而不會有您在網頁輸出中所看到的多餘元素。  
  
 若要使用用戶端列印功能，您必須安裝 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX 控制項。 如需詳細資訊，請參閱 [啟用和停用 Reporting Services 的用戶端列印](../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="print-options"></a>列印選項  
 若要在 **[列印]** 對話方塊中設定報表的列印屬性，請按一下 **[屬性]** 按鈕。 **[紙張大小]** 會由報表定義中所定義之報表頁面大小的預設高度和寬度來決定。 可用的值將視印表機類型及其功能而定。 [寬度] 和 [高度] 會顯示電腦上已設定之列印驅動程式的預設值。 變更這些值會導致報表使用新的尺寸來列印。 頁寬和頁高會由 **[方向]**決定，方向會設為 **[縱向]** 或 **[橫向]**。 所顯示的預設方向會視報表的頁寬和頁高而定。  
  
> [!NOTE]  
>  **[列印]** 對話方塊和預設的印表機設定 (頁寬、頁高及頁面方向等)，會由報表定義來決定。  
  
### <a name="print-preview"></a>預覽列印  
 若要在 **[列印]** 對話方塊中預覽報表，請按一下 **[預覽]** 按鈕。 按一下預覽會以個別的預覽視窗，來開啟報表的第一頁。 其他的頁面在報表於報表伺服器上完成轉譯之後即可使用。 預覽的報表會轉譯成 EMF 格式。 您可以導覽至上一頁或下一頁，直到出現最後一頁為止，此時 **[下一頁]** 按鈕就會停用。  
  
### <a name="adjusting-print-margins"></a>調整列印邊界  
 您可以在列印轉譯的 EMF 報表之前，先在該報表中修改列印邊界。 若要這樣做，請在 **[列印]** 對話方塊中，按一下 **[預覽]** 按鈕。 在預覽頁面頂端，按一下 **[邊界]** 按鈕。 [邊界] 對話方塊隨即顯示。 請設定您要的上、下、左、右邊界。 [!INCLUDE[clickOK](../../includes/clickok-md.md)] 對話方塊會關閉並儲存設定，以供轉譯預覽和列印使用。  
  
## <a name="see-also"></a>請參閱＜  
 [列印報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)   
 [列印報表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-builder/print-a-report-report-builder-and-ssrs.md)  
  
  
