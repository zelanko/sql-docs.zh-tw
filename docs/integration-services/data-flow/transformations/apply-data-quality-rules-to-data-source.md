---
title: "資料品質規則套用至資料來源 |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a965e8f2-004d-4ccc-8523-a185b35b26e2
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e7db6b5fc01c5d85b75ebdd6c78ba004a94135bf
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="apply-data-quality-rules-to-data-source"></a>將資料品質規則套用至資料來源
  您可以使用 Data Quality Services (DQS) 修正封裝資料流程中的資料，方法是將 DQS 清理轉換連接至資料來源。 如需有關 DQS 的詳細資訊，請參閱＜ [Data Quality Services Concepts](../../../data-quality-services/data-quality-services-concepts.md)＞。 如需此轉換的詳細資訊，請參閱＜ [DQS Cleansing Transformation](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)＞。  
  
 當您使用 DQS 清理轉換處理資料時，會在資料品質伺服器上建立資料品質專案。 您可以使用 Data Quality Client 管理專案。 如需詳細資訊，請參閱 [開啟、解除鎖定、重新命名和刪除資料品質專案](https://msdn.microsoft.com/library/hh510417.aspx)。  
  
### <a name="to-correct-data-in-the-data-flow"></a>若要更正資料流程中的資料  
  
1.  建立封裝。  
  
2.  加入並設定 DQS 清理轉換。 如需相關資訊，請參閱 [DQS Cleansing Transformation Editor Dialog Box](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation-editor-dialog-box.md)。  
  
3.  將 DQS 清理轉換連接至資料來源。  
  
  
