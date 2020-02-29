---
title: 工作6：將 Excel 來源加入至資料流程 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 0209055e-cb6b-4a07-909e-836596727a2c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: eff79fb144c2bbc4d31a21b2dc263c4ccb087104
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/28/2020
ms.locfileid: "78177236"
---
# <a name="task-6-adding-excel-source-to-the-data-flow"></a>工作 6：將 Excel 來源加入至資料流程
  在這項工作中，您會將 Excel 來源加入至資料流程，以便從來源 Excel 檔案讀取供應商資料。 Excel 來源會從 Microsoft Excel 活頁簿中的工作表或範圍擷取資料。 如需詳細資訊，請參閱[Excel 來源](../integration-services/data-flow/excel-source.md)主題。

1.  從 [ **SSIS 工具箱**] 中的 [**其他來源**] 將 [ **Excel 來源**] 拖放至 [**資料流程**] 索引標籤。

2.  以滑鼠右鍵**按一下 [資料流程**] 索引標籤中的 [ **Excel 來源**]，然後按一下 [**重新命名**]。

3.  輸入**從 Excel 檔案讀取供應商資料**，然後按**enter**鍵。

4.  按兩下 [**從 excel 檔案讀取供應商資料**]，啟動 [ **excel 來源編輯器**] 對話方塊。

5.  在 [ **Excel 來源編輯器**] 對話方塊中，按一下 [**新增**] 以建立 Excel 連接。

6.  在 [ **Excel 連接管理員**] 對話方塊中，按一下 [**流覽]**，然後選取 [ **EIM 教學**課程] 資料夾中的**供應商 .xls**檔案。 確認已在 [ **Excel 版本**] 方塊中選取 [ **Microsoft Excel 97-2003** ]，然後按一下 **[確定]**。

     ![Excel 連接管理員對話方塊](../../2014/tutorials/media/et-addingexcelsourcetothedataflow-01.jpg "Excel 連接管理員對話方塊")

7.  在 [ **Excel 來源編輯器**] 對話方塊中，于 [ **excel 工作表的名稱**] 清單方塊中選取 [ **IncomingSuppliers $** ]。

     ![Excel 工作表名稱 - 進貨供應商$](../../2014/tutorials/media/et-addingexcelsourcetothedataflow-02.jpg "Excel 工作表名稱 - 進貨供應商$")

8.  按一下 [**預覽**] 以預覽 Excel 檔案中的資料。

9. 按一下 **[確定]** ，關閉對話方塊。

10. 在 [ **SSIS 工具箱**] 的**其他轉換**中，將**DQS 清理**轉換拖放至 [**從 Excel 檔案讀取供應商資料**] 底下的 [**資料流程**] 索引標籤。 DQS 清理轉換會使用 Data Quality Services (DQS)，藉由套用知識庫中核准的規則來更正資料。 這項轉換在執行階段會在 DQS 伺服器上建立 DQS 清理專案。 如需詳細資訊，請參閱[DQS 清理轉換](https://msdn.microsoft.com/library/ee677619.aspx)主題。

## <a name="next-step"></a>後續步驟

[工作 7：將 DQS 清理轉換加入至資料流程](task-7-adding-dqs-cleansing-transform-to-the-data-flow.md)

### <a name="see-also"></a>另請參閱

[資料流程](../integration-services/data-flow/data-flow.md)
