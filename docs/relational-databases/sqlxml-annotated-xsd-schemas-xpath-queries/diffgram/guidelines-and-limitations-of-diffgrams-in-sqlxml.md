---
title: 方針和限制的 DiffGrams 的 SQLXML |Microsoft 文件
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: cf8689c4-2a63-4d05-b202-21b5ff187d7f
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9f63bc4259d60cdca7a82057dacafad21573156a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32967263"
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>在 SQLXML 中的 DiffGrams 指導方針和限制
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  搭配 SQLXML 4.0 使用 DiffGrams 時，請記住以下事項：  
  
-   二進位大型物件 (BLOB) 類型如同**text/ntext**映像不應使用在 **\<before>： 之前 >** 區塊時使用 DiffGrams，因為這會將它們包含在中使用並行存取控制。 這可能會因為 BLOB 類型的比較限制而造成 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的問題。 例如，LIKE 關鍵字用於 WHERE 子句中的資料行之間的比較**文字**資料類型; 不過，比較將會失敗如果 BLOB 類型中的資料大小大於 8k。  
  
-   中的特殊字元**ntext**資料可以會因為 BLOB 類型的比較限制而造成 SQLXML 4.0 的問題。 例如，使用"[Serializable]"中的 **\<before>： 之前 >** DiffGram 時的資料行的並行檢查中使用的區塊**ntext**類型會因下列 SQLOLEDB錯誤描述：  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  
