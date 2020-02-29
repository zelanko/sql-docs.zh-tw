---
title: 設定報表的一般屬性（報表管理員） |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], properties
- properties [Reporting Services], general
ms.assetid: 10b941b2-28e6-4408-9ee4-acebc63c8496
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 23184e77efbe41eae3d4de434a30ff8f3a4847ff
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/28/2020
ms.locfileid: "78177028"
---
# <a name="configure-general-properties-for-a-report-report-manager"></a>設定報表的一般屬性 (報表管理員)
  
### <a name="to-configure-general-report-properties"></a>若要設定一般報表屬性

1.  啟動 [報表管理員 &#40;SSRS 原生模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)。

2.  在報表管理員中，導覽至 **[內容]** 頁面。 導覽到您要設定一般屬性的報表，並開啟該報表。

3.  按一下 [屬性]  索引標籤。

     或者，如果 [**內容**] 頁面是在詳細資料檢視中，請按一下 [屬性頁] 圖示：

     ![屬性頁圖示](media/prop.gif "屬性頁面圖示")

4.  [**一般**屬性] 頁面隨即顯示，而且您可以設定屬性，如下所示：

    -   在 [**屬性**] 區段中，您可以修改報告名稱和描述。

    -   您可以選取 [**在清單視圖中隱藏**] 核取方塊，在頁面以預設頁面配置（[清單視圖]）中開啟時隱藏專案，這會在頁面上和向下排列專案。

    -   在 [**報表定義**] 區段中，按一下 [**編輯**]，將報表定義的複本解壓縮。 您在本機對報表定義所做的修改不會儲存在報表伺服器上。

         或者，若要從 .rdl 檔案更新報表定義，請按一下 [**更新**]。

        > [!NOTE]
        >  如果更新報表定義，必須在完成更新之後重設資料來源設定。

    -   使用 [**刪除**] 或 [**移動**] 按鈕來刪除或移動報表。

    -   您也可以建立連結報表。

5.  當您完成設定報表的一般屬性時，**請按一下 [** 套用]。

## <a name="see-also"></a>另請參閱
 [移動或刪除專案 &#40;報表管理員&#41;](report-server/move-or-delete-an-item-report-manager.md) [內容] 頁面 &#40;報表管理員](../../2014/reporting-services/contents-page-report-manager.md)&#41;[尋找、查看和管理報表 &#40;報表產生器和 SSRS &#41;](report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md) [一般屬性頁面、報表 &#40;報表管理員&#41;](../../2014/reporting-services/general-properties-page-reports-report-manager.md)


