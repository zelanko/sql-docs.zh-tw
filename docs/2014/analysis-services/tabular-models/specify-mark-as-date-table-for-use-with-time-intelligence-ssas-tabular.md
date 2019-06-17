---
title: 指定標記為日期資料表以搭配時間智慧使用 （SSAS 表格式） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 30841d1f-0c3b-4575-8f4a-27a1492e248c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0a39cbc319b7b0a62f31b55ded8adfe60a49314b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66066563"
---
# <a name="specify-mark-as-date-table-for-use-with-time-intelligence-ssas-tabular"></a>指定標記為日期資料表以搭配時間智慧使用 (SSAS 表格式)
  若要在 DAX 公式中使用時間智慧函數，您必須指定日期資料表以及 Date 資料類型的唯一識別碼 (日期時間) 資料行。 您將日期資料表中的某個資料行指定為唯一識別碼之後，就可以在日期資料表與任何事實資料表的資料行之間建立關聯性。  
  
 使用時間智慧函數時，適用下列規則：  
  
-   使用 DAX 時間智慧函數時，請勿指定事實資料表中的日期時間資料行。 請務必在您的模型中建立個別的日期資料表，其中至少包含一個 Date 資料類型的日期時間資料行且包含唯一值。  
  
-   請確定您的日期資料表具有連續的日期範圍。  
  
-   日期資料表中的日期時間資料行應該具有日資料粒度 (不含日的分數部分)。  
  
-   您必須使用 **[標記為日期資料表]** 對話方塊來指定日期資料表和唯一識別碼資料行。  
  
-   在事實資料表與日期資料表中 Date 資料類型的資料行之間建立關聯性。  
  
#### <a name="to-specify-a-date-table-and-unique-identifier"></a>若要指定日期資料表和唯一識別碼  
  
1.  在模型設計師中，按一下日期資料表。  
  
2.  依序按一下 **[資料表]** 功能表、 **[日期]** 和 **Mark as [日期] [資料表]** 。  
  
3.  在 **[標記為日期資料表]** 對話方塊的 **[日期]** 清單方塊中，選取要當做唯一識別碼使用的資料行。 這個資料行必須包含唯一值而且應該屬於 Date 資料類型。 例如：  
  
    |Date|  
    |----------|  
    |7/1/2010 12:00:00 AM|  
    |7/2/2010 12:00:00 AM|  
    |7/3/2010 12:00:00 AM|  
    |7/4/2010 12:00:00 AM|  
    |7/5/2010 12:00:00 AM|  
  
4.  必要時，請在事實資料表與日期資料表之間建立任何關聯性。  
  
## <a name="see-also"></a>另請參閱  
 [計算 &#40;SSAS 表格式&#41;](calculations-ssas-tabular.md)   
 [時間智慧函數&#40;DAX&#41;](https://msdn.microsoft.com/library/ee634763.aspx)  
  
  
