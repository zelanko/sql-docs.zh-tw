---
title: 工作4：將比對活動的結果匯出至 Excel 檔案 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 644454c4-3c5a-469a-90ec-e51dc7fb99fc
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: fd85a523804232deff14f2e1da5485229f943dd2
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "84999661"
---
# <a name="task-4-exporting-the-results-from-matching-activity-to-an-excel-file"></a>工作 4：將比對活動的結果匯出到 Excel 檔案
  在這項工作中，您會將比對活動的結果匯出到 Excel 檔案。

1.  在 [**匯出**] 頁面中，針對 [**目的地類型**] 選取 [ **Excel**檔案]。

2.  選取 [**生存結果**] 選項。 在生存程式中，DQS 會根據您選取的**生存規則**，決定每個叢集的生存者記錄。

3.  按一下 **[流覽]** ，並流覽至您要儲存輸出檔案的資料夾。

4.  針對名稱輸入**清理和相符的 Suppliers.xls** ，然後按一下 [**開啟**]。

5.  確認已選取 [**生存] 規則**的 [**樞紐分析表記錄**]。 當您選取此選項時，便會針對叢集的輸出挑選每個叢集的樞紐記錄。 存活規則的其他選項包括：

    1.  **最完整的記錄：** 生存者記錄是已填入最多欄位的記錄。

    2.  **最長的記錄：** 生存者記錄是來源欄位中具有最大詞彙數目的記錄。

    3.  **最完整且最長的記錄：** 生存者記錄是已填入最多欄位數目，而且每個欄位中的詞彙數目最大值。

     ![[匯出比對結果] 頁面](../../2014/tutorials/media/et-exportingtheresultsfrommatoanexcelfile.jpg "[匯出比對結果] 頁面")

6.  按一下 [**匯出**]，將結果匯出至 Excel 檔案。

7.  按一下 [**關閉**] 以關閉 [比對**匯出**] 對話方塊。

8.  按一下 **[完成]** 完成比對活動。

9. 開啟**清理並**比對 Suppliers.xlsx檔案，並確認您看不到任何重複專案（已「可」）。

 現在，您的供應商資料已經清理和比對，以移除重複項。

## <a name="next-step"></a>後續步驟
 [第 4 課：在 MDS 中儲存供應商資料](../../2014/tutorials/lesson-4-storing-supplier-data-in-mds.md)


