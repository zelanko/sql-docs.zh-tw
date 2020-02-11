---
title: 將資料從 MDS 載入 Excel 中 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: dd29389b-928c-4e50-995c-c6af27f97805
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: bbe1188773d0770ff345cd54ea47e03a3c05555f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "65482708"
---
# <a name="load-data-from-mds-into-excel"></a>將資料從 MDS 載入 Excel 中
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]在中，您必須從 MDS 儲存機制載入資料，才能使用它。  
  
 如果您想要在載入之前篩選資料集，請[先參閱先篩選資料，然後再載入適用于 Excel 的 &#40;MDS 增益集&#41;](filter-data-before-exporting-mds-add-in-for-excel.md) 。  
  
## <a name="prerequisites"></a>Prerequisites  
 若要執行此程序：  
  
-   您必須擁有存取 **[總管]** 功能區域的權限。  
  
### <a name="to-load-data-from-mds-into-excel"></a>若要將資料從 MDS 載入 Excel 中  
  
1.  開啟 Excel，然後在 **[主要資料]** 索引標籤上，連接到 MDS 儲存機制。 如需詳細資訊，請參閱[連接到 MDS 儲存機制 &#40;適用於 Excel 的 MDS 增益集&#41;](connect-to-an-mds-repository-mds-add-in-for-excel.md)。  
  
2.  在 **[主資料總管]** 窗格中，選取模型和版本。 系統就會填入實體的清單。  
  
    -   如果沒有顯示 **[主資料總管]** 窗格，請按一下 **[連接和載入]** 群組中的 **[顯示總管]**。  
  
    -   如果 **[主資料總管]** 窗格已停用，這是因為現有的工作表已經包含 MDS 管理的資料。 若要啟用此窗格，請開啟新的工作表。  
  
3.  在 [主資料總管]**** 窗格的實體清單中，按兩下您想要載入的實體。  
  
    > [!NOTE]  
    >  -   只有前 1 百萬個成員會載入 Excel 中。 若要在載入之前篩選清單，在功能區上，按一下 [連接和載入]**** 群組中的 [篩選]****。  
    > -   在屬於受條件約束之清單 (網域屬性) 的資料行中，只會載入前 25,000 個值。 您可以在安裝 Excel 所在電腦上的 excelusersettings.config 檔案內，變更 MaximumDbaEntitySize 屬性中的這個數字。 此檔案位於 C:\Users\\<USER\>\AppData\Local\Microsoft\Microsoft SQL Server\120\MasterDataServices。\\  
  
    > [!NOTE]  
    >  如果您使用適用於 Microsoft Excel (32 位元 Excel) 的增益集載入以文字分隔的資料，而且 [Cell Count to Load (要載入的資料格計數)]**** 和 [Cell Count to Publish (要發行的資料格計數)]**** 屬性的值都設為最大值 1000，將會發生記憶體不足的錯誤。 您必須使用 64 位元 Excel，才能使用 [Cell Count to Load (要載入的資料格計數)]**** 和 [Cell Count to Publish (要發行的資料格計數)]**** 的最大值設定。  
  
## <a name="next-steps"></a>後續步驟  
 [將 Excel 的資料發行至適用于 Excel 的 mds 增益集 &#40;&#41;](import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>另請參閱  
 [載入適用于 Excel 的 MDS 增益集&#41;的資料 &#40;](overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [[篩選] 對話方塊 &#40;適用于 Excel 的 MDS 增益集&#41;](filter-dialog-box-mds-add-in-for-excel.md)   
 [發行資料 &#40;適用于 Excel 的 MDS 增益集&#41;](overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  
