---
title: 瀏覽報表組件及設定預設資料夾 (報表產生器及 SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 5cf38068-65d1-4fe8-81f3-a404d8fbc663
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2eef96c7bde16746a91fe53f94adb19bbadadf2e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "65581831"
---
# <a name="browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs"></a>瀏覽報表組件及設定預設資料夾 (報表產生器及 SSRS)
建立 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 分頁報表最簡單的方式，就是從報表組件庫將現有的報表組件 (例如資料表和圖表) 加入您的報表。 當您將報表組件加入到報表時，您也會加入此組件運作所必須擁有的所有項目。 例如，顯示資料的所有報表組件都取決於資料集，也就是資料來源的查詢和連接。 當您將報表組件加入至報表之後，您可以盡量修改它。  
  
 您可以設定預設資料夾，以便將報表組件發行到報表伺服器或與報表伺服器整合的 SharePoint 網站。  
  
 如需詳細資訊，請參閱 [報表組件 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)。  
  
## <a name="to-browse-for-report-parts"></a>若要瀏覽報表組件  
  
1.  在 [插入]  功能表上，按一下 [報表組件]  。  
  
     如果您尚未連線，請按一下 [連線到報表伺服器]  ，並輸入名稱。  
  
    > [!NOTE]  
    >  您必須連接到報表伺服器，才能瀏覽報表組件。  
  
2.  您可以指定報表組件的詳細資料來縮小搜尋範圍。 請在 [搜尋]  方塊中鍵入完整名稱或名稱的一部分和描述，或是按一下 [新增準則]  並針對任何欄位或所有欄位新增值：  
  
    -   建立者  
  
    -   建立日期  
  
    -   上次修改日期  
  
    -   上次修改者  
  
    -   伺服器資料夾  
  
    -   類型  
  
     例如，若要尋找影像，請按一下 [新增準則]  ，然後按一下 [類型]  。 在下拉式方塊中，選取 [影像]  核取方塊，按 ENTER ，然後按一下「搜尋」放大鏡。  
  
    > [!NOTE]  
    >  針對 [建立者]  和 [上次修改者]  值，搜尋此人員在報表伺服器上所代表的使用者名稱。  
  
## <a name="to-set-a-default-folder-for-report-parts"></a>若要設定報表組件的預設資料夾  
  
1.  按一下 [報表產生器]  ，然後按一下 [選項]  。  
  
2.  在 [選項]  對話方塊的 [設定]  索引標籤上，於 [將報表組件預設發行到此資料夾]  文字方塊中鍵入資料夾名稱。  
  
 如果此資料夾尚未存在，而且您有權在報表伺服器上建立資料夾，報表產生器將會建立這個資料夾。  
  
 您不需要重新啟動報表產生器，這項設定也會生效。  
  
## <a name="see-also"></a>另請參閱  
 [檢查更新或關閉更新 (報表產生器及 SSRS)](https://msdn.microsoft.com/9c69792d-d7c4-453b-ae2f-6d2d071d8606)   
 [報表組件 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)   
 [報表產生器中的報表組件和資料集](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md)   
 [針對報表組件進行疑難排解 (報表產生器及 SSRS)](https://msdn.microsoft.com/d9fe1932-46e7-421b-a8a9-4c54d9576e94)   
 [發行與重新發行報表組件 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/publish-and-republish-report-parts-report-builder-and-ssrs.md)  
  
  
