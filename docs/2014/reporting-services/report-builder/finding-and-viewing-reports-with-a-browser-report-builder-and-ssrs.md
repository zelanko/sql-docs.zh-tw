---
title: 使用瀏覽器尋找及檢視報表 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: edf4843a-2a0a-486f-be25-14a3c1c6bc72
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: c91d12665ac8637f9de407896aed435a02af6940
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53365167"
---
# <a name="finding-and-viewing-reports-with-a-browser-report-builder-and-ssrs"></a>使用瀏覽器尋找及檢視報表 (報表產生器及 SSRS)
  您可以使用任何支援的網頁瀏覽器，透過報表伺服器的直接連接來檢視報表。 每一個報表在報表伺服器上都有一個 URL 位址。 您可以輸入報表的 Web 位址，在任何 Web 應用程式的瀏覽器視窗中開啟該報表。 該報表會以 HTML 格式開啟，而且其中包含報表工具列，讓您可以在報表中瀏覽頁面或搜尋資料值。 您可以在 URL 上設定參數，以隱藏工具列或選取報表的輸出格式。  
  
 透過報表的 Web 位址來開啟報表適合檢視報表，但不適合管理報表。 您無法存取項目的屬性頁或訂閱定義頁面。 您必須使用「報表管理員」或 SharePoint 網站處理這些工作。  
  
 如果您不知道報表的 Web 位址，您可以開啟報表伺服器的 Web 位址，然後瀏覽報表伺服器的資料夾階層，以選取您要檢視的報表。 下圖說明瀏覽器視窗中所顯示的資料夾階層。  
  
 ![瀏覽器中的資料夾](../media/rs-browserfolder.GIF "瀏覽器中的資料夾")  
瀏覽器中的資料夾  
  
> [!NOTE]  
>  如果您要從手持式裝置存取報表，就必須使用瀏覽器來開啟報表。 報表管理員的設計不適用於手持式裝置。  
  
 如需您可以使用之瀏覽器類型的詳細資訊，請參閱《SQL Server 線上叢書》中 [Reporting Services 文件集](https://go.microsoft.com/fwlink/?linkid=121312) 的＜Reporting Services 所支援的瀏覽器類型＞。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="navigating-report-server-folders-in-a-web-browser"></a>在網頁瀏覽器中導覽報表伺服器資料夾  
 您可以使用網頁瀏覽器來導覽報表伺服器資料夾以及執行報表。 報表和項目在資料夾階層中，會以連結顯示。 您可以按一下連結以開啟報表、資源或資料夾，或檢視共用資料來源的內容。 若您不知道報表的 URL，則導覽資料夾階層很有用。 您可以指定讓報表伺服器的 Web 位址，使用瀏覽器開啟資料夾階層的根節點連接，然後按一下資料夾的連結來導覽階層。  
  
 當您存取報表伺服器的虛擬目錄時，只可以查看您有權存取的資料夾、報表和上傳的項目。 使用者介面只會顯示資料夾階層和基本資訊，例如個別項目的建立或修改日期、檔案大小和項目類型：  
  
-   沒有其他指標的連結就是報表或模型。  
  
-   \<ds> 標記代表共用資料來源。  
  
-   \<dir> 標記代表資料夾項目。  
  
-   副檔名代表資源。 副檔名可識別資源的 MIME 類型。 例如，.jpg 代表 JPEG 格式的影像。  
  
## <a name="typing-the-url-address-of-a-report"></a>輸入報表的 URL 位址  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 支援對報表伺服器上的特定項目進行 URL 存取。 URL 必須包含報表和命令的完整路徑，才能轉譯報表。 如果報表包含參數，您也必須指定開啟報表所需的任何值。 如果您要輸入的報表 URL 之路徑、參數值或轉譯延伸模組中含有空格，就必須將 URL 已編碼的字元納入 URL 中，才能獲得預期的結果。 下列範例呈現在報表 URL 中的路徑名稱、參數和轉譯延伸模組中含有空格時，所使用的編碼：  
  
 `http://<Webservername>/reportserver?/<reportfolder>/employee+sales+summary&ReportYear=2004&ReportMonth=06&EmpID=24&rs:Command=Render&rs:Format=HTML4.0`  
  
 URL 在 Internet Explorer 中的限制上限為 2,083 個字元。 如需詳細資訊，請參閱 [Internet Explorer 的 URL 長度上限](https://support.microsoft.com/kb/208427)。  
  
 如需如何透過 URL 存取報表的詳細資訊，包括如何建構 URL 的資訊，請參閱《SQL Server 線上叢書》中 [Reporting Services 文件集](https://go.microsoft.com/fwlink/?linkid=121312)的＜URL 存取＞。  
  
## <a name="see-also"></a>另請參閱  
 [尋找及檢視報表在報表管理員中&#40;報表產生器及 SSRS&#41;](finding-and-viewing-reports-in-the-web-portal-report-builder-and-ssrs.md)  
  
  
