---
title: 指定外部項目的路徑 (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 4fe513da-f3c5-479c-9fec-8662b91a0d6d
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 590b8f44e1d3ba064176bf8944c4011fbf52ab53
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56297966"
---
# <a name="specifying-paths-to-external-items-report-builder-and-ssrs"></a>指定外部項目的路徑 (報表產生器及 SSRS)
  您可以在報表項目屬性中指定路徑，以便參考位於報表定義檔案外部且儲存在報表伺服器上的項目，例如鑽研報表、子報表和影像檔。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
> [!NOTE]  
>  在報表產生器中，項目的路徑必須指定報表伺服器上的項目。 不支援檔案系統上之項目的路徑。 只有當您已連接至項目所在的報表伺服器時，才能預覽使用這些項目的報表。  
  
 當您在動作、子報表或影像的對話方塊中指定外部項目的路徑時，可以直接瀏覽至報表伺服器並選取此項目。 直接瀏覽至項目並選取項目是指定鑽研報表或子報表的建議方式。 若使用這種方式，當您指定報表或子報表參數時，下拉式清單就會提供正確的參數名稱。 當您變更項目路徑來指向不同的項目時，則必須視需要手動更新正確的參數名稱和值。  
  
 在設定為原生模式的報表伺服器上，請指定不含副檔名 .rdl 的鑽研報表名稱。  
  
 在設定為 SharePoint 整合模式的報表伺服器上，您必須包含副檔名 .rdl。 路徑可以是下列其中一項：  
  
-   **來自主報表之項目的相對路徑。** 例如 ../AllSubreports/Subreport1。 在此範例中， **..** 表示主報表所在之資料夾上方的資料夾。  
  
    > [!NOTE]  
    >  在報表產生器內部執行報表時，不支援相對路徑。 若要檢視使用外部項目之相對路徑的報表，請將報表儲存至報表伺服器，然後從中執行報表。  
  
-   **項目的完整路徑。**  
  
    -   **在報表伺服器：** 路徑的開頭**/**，主資料夾 資料夾。 例如 /Reports/AllSubreports/Subreport1。  
  
    -   **在 SharePoint 網站：** 在運算式中，項目和副檔名.rdl 的完整 url，您必須指定報表名稱。 例如， `="http://server/site/library/folder/Report1.rdl"` 。  
  
## <a name="see-also"></a>另請參閱  
 [加入外部影像 &#40;報表產生器及 SSRS&#41;](add-an-external-image-report-builder-and-ssrs.md)   
 [加入子報表和參數 &#40;報表產生器及 SSRS&#41;](add-a-subreport-and-parameters-report-builder-and-ssrs.md)   
 [在報表上新增鑽研動作 &#40;報表產生器及 SSRS&#41;](add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md)  
  
  
