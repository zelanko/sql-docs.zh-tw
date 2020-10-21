---
description: 將資料品質規則套用至資料來源
title: 將資料品質規則套用至資料來源 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a965e8f2-004d-4ccc-8523-a185b35b26e2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: afccf7296d27331d7b76ba5e4978faca2126060f
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194652"
---
# <a name="apply-data-quality-rules-to-data-source"></a>將資料品質規則套用至資料來源

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  您可以使用 Data Quality Services (DQS) 修正封裝資料流程中的資料，方法是將 DQS 清理轉換連接至資料來源。 如需有關 DQS 的詳細資訊，請參閱＜ [Data Quality Services Concepts](../../../data-quality-services/data-quality-services-concepts.md)＞。 如需此轉換的詳細資訊，請參閱＜ [DQS Cleansing Transformation](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)＞。  
  
 當您使用 DQS 清理轉換處理資料時，會在資料品質伺服器上建立資料品質專案。 您可以使用 Data Quality Client 管理專案。 如需詳細資訊，請參閱 [開啟、解除鎖定、重新命名和刪除資料品質專案](../../../data-quality-services/open-unlock-rename-and-delete-a-data-quality-project.md)。  
  
### <a name="to-correct-data-in-the-data-flow"></a>若要更正資料流程中的資料  
  
1.  建立封裝。  
  
2.  加入並設定 DQS 清理轉換。 如需相關資訊，請參閱 [DQS Cleansing Transformation Editor Dialog Box](./dqs-cleansing-transformation.md)。  
  
3.  將 DQS 清理轉換連接至資料來源。  
  
