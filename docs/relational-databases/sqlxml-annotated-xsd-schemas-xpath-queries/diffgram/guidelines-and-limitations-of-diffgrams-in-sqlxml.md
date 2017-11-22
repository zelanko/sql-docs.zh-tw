---
title: "方針和限制的 DiffGrams 的 SQLXML |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: DiffGrams [SQLXML], about DiffGrams
ms.assetid: cf8689c4-2a63-4d05-b202-21b5ff187d7f
caps.latest.revision: "7"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 07f698a9bcd18566d4cca639e810056f79523684
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>在 SQLXML 中的 DiffGrams 指導方針和限制
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]搭配 SQLXML 4.0 使用 DiffGrams 時，請記住下列事項：  
  
-   二進位大型物件 (BLOB) 類型如同**text/ntext**映像不應使用在 **\<before>： 之前 >**區塊時使用 DiffGrams，因為這會將它們包含在中使用並行存取控制。 這可能會因為 BLOB 類型的比較限制而造成 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的問題。 例如，LIKE 關鍵字用於 WHERE 子句中的資料行之間的比較**文字**資料類型; 不過，比較將會失敗如果 BLOB 類型中的資料大小大於 8k。  
  
-   中的特殊字元**ntext**資料可以會因為 BLOB 類型的比較限制而造成 SQLXML 4.0 的問題。 例如，使用"[Serializable]"中的 **\<before>： 之前 >** DiffGram 時的資料行的並行檢查中使用的區塊**ntext**類型會因下列 SQLOLEDB錯誤描述：  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  
