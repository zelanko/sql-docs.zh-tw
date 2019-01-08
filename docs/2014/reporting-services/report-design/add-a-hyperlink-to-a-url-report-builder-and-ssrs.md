---
title: 將超連結新增到 URL (報表產生器及 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: d3392c0b-7b62-4d27-bc04-2bd0c5487d08
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 1219998db8ec07de6e03aa14b3aefaee6515e235
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53366170"
---
# <a name="add-a-hyperlink-to-a-url-report-builder-and-ssrs"></a>將超連結加入到 URL (報表產生器及 SSRS)
  當您希望使用者能夠按一下報表中的連結，並開啟瀏覽器指向您所指定的 URL 時，可以將超連結加入到報表項目。 超連結可以是靜態 URL，或是評估為 URL 的運算式。 如果資料庫中有一個包含 URL 的欄位，運算式便能包含這個欄位，結果會在報表中產生超連結的動態清單。 您可以將超連結加入至文字方塊、影像、圖表和量測計。 您必須確定使用者可存取您提供的 URL。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 您也可以在您和您的使用者有權使用報表伺服器之 URL 要求進行檢視的任何報表伺服器上指定報表的 URL。 例如，您可以指定報表，並在使用者最初檢視報表時為他們隱藏文件引導模式。 如需詳細資訊，請參閱《[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》中 [Reporting Services 文件集](https://go.microsoft.com/fwlink/?linkid=121312)的 [URL 存取 &#40;SSRS&#41;](../url-access-ssrs.md)。  
  
 您可以將 URL 的超連結加入到具有 **[動作]** 屬性的任何項目，例如報表中的文字方塊、影像或導出數列。 當使用者按一下該報表項目時，就會發生您定義的動作。 如需詳細資訊，請參閱[動作屬性對話方塊 &#40;報表產生器及 SSRS&#41;](../action-properties-dialog-box-report-builder-and-ssrs.md) 和[指定外部項目的路徑 &#40;報表產生器及 SSRS&#41;](specifying-paths-to-external-items-report-builder-and-ssrs.md)。  
  
 若要快速開始使用，請參閱[教學課程：格式化文字&#40;報表產生器&#41;](../tutorial-format-text-report-builder.md)。  
  
> [!NOTE]  
>  繫結至資料集欄位的連結可能很容易受到惡意竄改。 如需詳細資訊，請參閱 msdn.microsoft.com 上 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][ 線上叢書](https://go.microsoft.com/fwlink/?LinkId=154888)中的[保護報表和資源的安全](../security/secure-reports-and-resources.md)。  
  
### <a name="to-add-a-hyperlink"></a>若要加入超連結  
  
1.  在報表設計檢視中，以滑鼠右鍵按一下要加入連結的文字方塊、影像或圖表，然後按一下 **[屬性]**。  
  
2.  在 [屬性] 對話方塊中，按一下 **[動作]**。  
  
3.  選取 **[移至 URL]**。 此對話方塊中會出現這個選項的其他區段。  
  
4.  在 **[選取 URL]** 中，輸入或選取 URL 或是評估為 URL 的運算式，或者按下拉式箭號，再按一下含有 URL 之欄位的名稱。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  (選擇性) 文字不會自動格式化為連結。 如果是文字，則變更文字色彩及效果來指示該文字為連結，將會是很有協助的作法。 例如，在 [功能區] 的 [主資料夾] 索引標籤上設定 **[字型]** 區段，將色彩變更為藍色並加上底線效果。  
  
7.  若要測試連結，請按一下 **[執行]** 預覽報表，然後按一下這個連結設定所在的報表項目。  
  
## <a name="see-also"></a>另請參閱  
 [互動式排序、文件引導模式及連結 &#40;報表產生器及 SSRS&#41;](interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [建立文件引導模式 &#40;報表產生器及 SSRS&#41;](create-a-document-map-report-builder-and-ssrs.md)  
  
  
