---
title: 資料品質比對資料行 (適用於 Excel 的 MDS 增益集) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: f683fdc6-0d4c-4793-8143-567616cb2094
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: ecbbaba1441fa150daaecbfcbc7cbdf65636de55
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "65482644"
---
# <a name="data-quality-matching-columns-mds-add-in-for-excel"></a>資料品質比對資料行 (適用於 Excel 的 MDS 增益集)
  在中，當您比對資料之後，您可以在功能區的 [**資料品質**] 群組中按一下 [**顯示詳細**資料]，以顯示提供相符詳細資料的資料行。 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]  
  
 下表顯示比對資料時所顯示的資料行。  
  
|名稱|描述|  
|----------|-----------------|  
|**CLUSTER_ID**|用於將相似記錄分組的唯一識別碼。 所有相似的資料列都有相同的 **CLUSTER_ID**。 如果沒有顯示資料列的 **CLUSTER_ID** ，表示找不到相似的記錄。|  
|**RECORD_ID**|用於識別記錄的唯一識別碼。 類似於 MDS 儲存機制中儲存的代碼值，它是用來識別記錄的值。 每次進行比對時，都會自動產生它。|  
|**PIVOT_MARK**|與其他記錄比較的任意記錄；它沒有分數值。|  
|**成績**|表示群組中的記錄與樞紐記錄的相似度。 此分數由 DQS 決定。 如果沒有顯示分數，表示記錄是其他記錄的樞紐，或是找不到相符結果。|  
  
## <a name="see-also"></a>另請參閱  
 [適用于 Excel 的 MDS 增益集中的資料品質比對](data-quality-matching-in-the-mds-add-in-for-excel.md)   
 [符合適用于 Excel&#41;的類似資料 &#40;MDS 增益集](match-similar-data-mds-add-in-for-excel.md)   
 [資料比對](../../data-quality-services/data-matching.md)  
  
  
