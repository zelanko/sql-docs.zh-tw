---
title: 資料品質比對資料行 (適用於 Excel 的 MDS 增益集) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f683fdc6-0d4c-4793-8143-567616cb2094
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 79af46616a685d8e52086c3621a963c350db7abf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36146561"
---
# <a name="data-quality-matching-columns-mds-add-in-for-excel"></a>資料品質比對資料行 (適用於 Excel 的 MDS 增益集)
  在[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]中，當您比對資料之後，可在功能區的 [資料品質] 群組中按一下 [顯示詳細資料]，以顯示提供比對詳細資料的資料行。  
  
 下表顯示比對資料時所顯示的資料行。  
  
|[屬性]|描述|  
|----------|-----------------|  
|**CLUSTER_ID**|用於將相似記錄分組的唯一識別碼。 所有相似的資料列都有相同的 **CLUSTER_ID**。 如果沒有顯示資料列的 **CLUSTER_ID** ，表示找不到相似的記錄。|  
|**RECORD_ID**|用於識別記錄的唯一識別碼。 類似於 MDS 儲存機制中儲存的代碼值，它是用來識別記錄的值。 每次進行比對時，都會自動產生它。|  
|**PIVOT_MARK**|與其他記錄比較的任意記錄；它沒有分數值。|  
|**SCORE**|表示群組中的記錄與樞紐記錄的相似度。 此分數由 DQS 決定。 如果沒有顯示分數，表示記錄是其他記錄的樞紐，或是找不到相符結果。|  
  
## <a name="see-also"></a>另請參閱  
 [資料品質比對中的 MDS 增益集的 Excel](data-quality-matching-in-the-mds-add-in-for-excel.md)   
 [比對相似資料 &#40;適用於 Excel 的 MDS 增益集&#41;](match-similar-data-mds-add-in-for-excel.md)   
 [資料比對](../../data-quality-services/data-matching.md)  
  
  