---
title: 取得資料連線的替代方式 (報表產生器) | Microsoft Docs
ms.date: 06/15/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.suite: pro-bi
ms.topic: conceptual
applies_to:
- SQL Server 2016
ms.assetid: aebc5f3d-97d5-4d54-b525-753fed073a9a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7b421f79dd45efdb7b9c0942b6611e88a0dbd7b9
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2018
ms.locfileid: "43272164"
---
# <a name="alternative-ways-to-get-a-data-connection-report-builder"></a>取得資料連接的替代方式 (報表產生器)
資料連接包含連接至外部資料來源的資訊，例如 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料庫。 通常您會向資料來源擁有者取得連接資訊以及要使用的認證類型。  
  
若要指定資料連接，您可以使用來自報表伺服器的共用資料來源，或是建立僅在特定報表中使用的內嵌資料來源。  
  
大部分的教學課程都是使用內嵌資料來源，但如果您具有共用資料來源的存取權，就可以改用後者這種資料來源。  
  
## <a name="getting-a-data-connection-from-a-shared-data-source"></a>從共用資料來源取得資料連接  
如果您有權限使用報表伺服器中可用的共用資料來源，則可以使用共用資料來源，而不使用內嵌資料來源。 下列程序說明如何尋找共用資料來源，並提供使用共用資料來源所需的任何認證。  
  
若要使用共用資料來源，您可以瀏覽至報表伺服器，並選取一個共用資料來源。 通常您可向報表伺服器管理員取得報表伺服器 URL。  
  
### <a name="to-specify-a-data-connection-from-a-list-of-shared-data-sources"></a>從共用資料來源清單指定資料連接  
  
1.  在 [新增資料表或矩陣精靈] 或 [新增圖表精靈] 的 [選擇資料集] 頁面上，選取 [建立資料集]，然後按一下 [下一步]。 **[選擇與資料來源的連接]** 頁面隨即開啟。  
  
2.  從資料來源清單中，選取您有權存取的資料來源。  
  
3.  若要確認您能夠連接至資料來源，請按一下 **[測試連接]**。 「成功建立連接」訊息就會出現。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
4.  按 [下一步] 。  
  
    如有需要，請輸入您的認證。 若要在本機儲存認證，請選取 [儲存連接的密碼]。 如果您未選取此選項，則會在每次執行報表時提示您提供認證  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-specify-a-data-connection-by-browsing-to-a-shared-data-source-on-a-report-server"></a>透過瀏覽報表伺服器上共用資料來源的方式指定資料連接  
  
1.  在 [新增資料表或矩陣精靈] 或 [新增圖表精靈] 的 [選擇資料集] 頁面上，選取 [建立資料集]，然後按一下 [下一步]。 **[選擇與資料來源的連接]** 頁面隨即開啟。  
  
2.  按一下 **[瀏覽]**。 [選取資料來源] 對話方塊隨即開啟。  
  
3.  從 [查詢] 下拉式清單中，選取 [最近使用的網站和伺服器]。 在資料來源窗格中，按一下伺服器的 URL，然後按一下 [開啟]。  
  
    資料來源或模型的清單隨即出現。  
  
4.  或者，在 [名稱] 中輸入報表伺服器的 URL。 按一下 **[開啟]**。  
  
    報表產生器會連接到報表伺服器，並且在根資料夾中載入可用的資料來源。  
  
5.  巡覽至包含您有足夠權限可連線之資料來源的資料夾，選取該資料來源，然後按一下 [開啟]。  
  
    您會回到 [選擇與資料來源的連線] 頁面。  
  
6.  若要確認您能夠連接至資料來源，請按一下 **[測試連接]**。  
  
    「成功建立連接」訊息就會出現。 [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  按 [下一步] 。  
  
8.  如果提示您提供使用者名稱和密碼，請輸入您的認證。 若要在本機儲存認證，請選取 [儲存連接的密碼]。  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
[報表資料集 &#40;SSRS&#41;](../reporting-services/report-data/report-datasets-ssrs.md)  
[報表產生器教學課程](../reporting-services/report-builder-tutorials.md) 
  

