---
title: 指定標記為日期資料表 |Microsoft 文件
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 30841d1f-0c3b-4575-8f4a-27a1492e248c
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 651dd51ca06e74b425b4d794da50276a001282c1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="specify-mark-as-date-table-for-use-with-time-intelligence"></a>指定標記為日期資料表以搭配時間智慧
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  若要在 DAX 公式中使用時間智慧函數，您必須指定日期資料表和唯一識別碼 (datetime) 資料行的日期資料類型。 您將日期資料表中的某個資料行指定為唯一識別碼之後，就可以在日期資料表與任何事實資料表的資料行之間建立關聯性。  
  
 使用時間智慧函數時，適用下列規則：  
  
-   使用 DAX 時間智慧函數時，請勿指定事實資料表的日期時間資料行。 請務必在您的模型中建立個別的日期資料表，其中至少包含一個 Date 資料類型的日期時間資料行且包含唯一值。  
  
-   請確定您的日期資料表具有連續的日期範圍。  
  
-   日期資料表中的日期時間資料行應該具有日資料粒度 (不含日的分數部分)。  
  
-   您必須使用 **[標記為日期資料表]** 對話方塊來指定日期資料表和唯一識別碼資料行。  
  
-   在事實資料表與日期資料表中 Date 資料類型的資料行之間建立關聯性。  
  
#### <a name="to-specify-a-date-table-and-unique-identifier"></a>若要指定日期資料表和唯一識別碼  
  
1.  在模型設計師中，按一下日期資料表。  
  
2.  依序按一下 **[資料表]** 功能表、 **[日期]** 和 **Mark as [日期] [資料表]**。  
  
3.  在 **[標記為日期資料表]** 對話方塊的 **[日期]** 清單方塊中，選取要當做唯一識別碼使用的資料行。 這個資料行必須包含唯一值而且應該屬於 Date 資料類型。 例如：  
  
    |日期|  
    |----------|  
    |7/1/2010 12:00:00 AM|  
    |7/2/2010 12:00:00 AM|  
    |7/3/2010 12:00:00 AM|  
    |7/4/2010 12:00:00 AM|  
    |7/5/2010 12:00:00 AM|  
  
4.  必要時，請在事實資料表與日期資料表之間建立任何關聯性。  
  
## <a name="see-also"></a>另請參閱  
 [計算](../../analysis-services/tabular-models/calculations-ssas-tabular.md)   
 [時間智慧函數 (DAX)](http://msdn.microsoft.com/en-us/91df278d-4b28-40c1-a572-cdb91f081517)  
  
  
