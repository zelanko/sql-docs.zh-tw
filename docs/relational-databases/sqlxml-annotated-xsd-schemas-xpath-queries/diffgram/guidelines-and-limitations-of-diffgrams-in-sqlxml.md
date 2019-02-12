---
title: 指導方針和限制的 DiffGrams 的 SQLXML |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: cf8689c4-2a63-4d05-b202-21b5ff187d7f
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2ce3283568cebebd81bc98b3d4ebba7ba81d46dd
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2019
ms.locfileid: "56041119"
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>在 SQLXML 中的 DiffGrams 指導方針和限制
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  搭配 SQLXML 4.0 使用 DiffGrams 時，請記住以下事項：  
  
-   二進位大型物件 (BLOB) 類型如同**text/ntext**中應不到映像 **\<before>： 之前 >** 區塊時使用 DiffGrams，因為這會將它們包含用於並行存取控制。 這可能會因為 BLOB 類型的比較限制而造成 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的問題。 比方說，LIKE 關鍵字用於 WHERE 子句中的資料行之間的比較**文字**資料類型; 不過，比較將會失敗如果資料的大小大於 8k 的 BLOB 類型。  
  
-   中的特殊字元**ntext**資料進行因為 BLOB 類型的比較限制，可能會造成某些搭配 SQLXML 4.0 的問題。 例如，"[Serializable]"中的使用 **\<before>： 之前 >** DiffGram 時用於並行存取檢查的資料行的區塊**ntext**類型將會失敗並下列 SQLOLEDB錯誤描述：  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  
