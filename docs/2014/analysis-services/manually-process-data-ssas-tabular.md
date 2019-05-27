---
title: 手動處理資料 (SSAS 表格式) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.datarefreshprogressdb.f1
ms.assetid: 0918c04c-c1e6-45b4-acfa-96fa578e684b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5de1215bd9646e115c6b2730c4e8a750a3f4040f
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66077966"
---
# <a name="manually-process-data-ssas-tabular"></a>手動處理資料 (SSAS 表格式)
  此主題描述如何手動處理 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中的工作空間資料。  
  
 當您撰寫使用外部資料的表格式模型時，可以使用處理命令來手動重新整理資料。 您可以處理單一資料表、模型中的所有資料表或是一個或多個資料分割。 每次處理資料時，您也可能需要重新計算資料。  處理資料表示從外部來源取得最新的資料。 重新計算表示更新使用資料之任何公式的結果。  
  
 本主題的章節：  
  
-   [手動處理資料](#bkmk_mahually_process)  
  
-   [資料處理進度](#bkmk_data_process_progress)  
  
##  <a name="bkmk_mahually_process"></a> 手動處理資料  
  
#### <a name="to-process-data-for-a-single-table-or-all-tables-in-a-model"></a>處理模型中單一資料表或所有資料表的資料  
  
1.  在模型設計師中，按一下要處理的資料表。  
  
2.  按一下 **[模型]** 功能表，然後按一下 **[處理]**，再按一下 **[處理]** 或 **[處理全部]**。  
  
#### <a name="to-process-data-for-all-tables-using-the-same-connection"></a>若要使用相同連接處理所有資料表的資料  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，按一下 **[模型]** 功能表，然後按一下 **[現有連接]**。  
  
2.  在 **[現有連接]** 對話方塊中，選取連接，然後按一下 **[處理]**。  
  
#### <a name="to-process-data-for-one-or-more-partitions"></a>若要處理一個或多個資料分割的資料  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，按一下 **[模型]** 功能表，然後指向 **[處理]**，再按一下 **[處理資料分割]**。  
  
2.  在 **[處理資料分割]** 對話方塊的 **[模式]** 中，選取下列其中一個處理模式：  
  
    |[模式]|描述|  
    |----------|-----------------|  
    |**處理預設**|偵測資料分割物件的處理狀態，並且執行必要的處理，以便將尚未處理或部分處理的資料分割物件傳遞為完整處理的狀態。 載入空白資料表和資料分割的資料；建立或重新建立階層、導出資料行及關聯性。|  
    |**完整處理**|處理資料分割物件及其包含的所有物件。 對已處理過的物件執行完整處理時， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 會先卸除該物件中的所有資料，然後再處理該物件。 當物件已進行過任何結構性變更時，就需要這種處理。|  
    |**處理資料**|將資料載入資料分割或資料表，而不重新建立階層或關聯性，或重新計算導出資料行和量值。|  
    |**處理清除**|移除資料分割中的所有資料。|  
    |**處理加入**|以新資料累加地更新資料分割。|  
  
3.  在資料分割清單中，選取要處理的資料分割，然後按一下 **[確定]**。  
  
##  <a name="bkmk_data_process_progress"></a> 資料處理進度  
 **[資料處理進度]** 對話方塊可讓您監視您已經從外部來源匯入模型之資料的處理作業。 若要存取此對話方塊，請按一下 **[模型]** 功能表，然後按一下 **[處理資料分割]**、 **[處理資料表]** 或 **[處理全部]**。  
  
 **狀態**  
 指出處理作業是否成功。  
  
 **詳細資料**  
 列出已匯入的資料表和檢視表、已匯入的資料列數目，並提供任何問題報告的連結。  
  
 **停止重新整理**  
 按一下可暫停處理作業。 如果作業耗費時間過長，或者如果有太多錯誤，這個選項會很有用。  
  
## <a name="see-also"></a>另請參閱  
 [處理資料 &#40;SSAS 表格式&#41;](process-data-ssas-tabular.md)   
 [疑難排解處理資料 &#40;SSAS 表格式&#41;](troubleshoot-process-data-ssas-tabular.md)  
  
  
