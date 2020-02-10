---
title: SQLXML 中的 Diffgram 指導方針和限制 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: cf8689c4-2a63-4d05-b202-21b5ff187d7f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a1113bf11fcb3b1be2164bc6e685e6454323f3df
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66013054"
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>在 SQLXML 中的 DiffGrams 指導方針和限制
  搭配 SQLXML 4.0 使用 DiffGrams 時，請記住以下事項：  
  
-   二進位大型物件 (BLOB) 類型如同 `text/ntext` 和 images，在使用 DiffGrams 時，不得用於 `<diffgr:before>` 區塊，因為這會將它們包含在並行控制中使用。 這可能會因為 BLOB 類型的比較限制而造成 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的問題。 例如，WHERE 子句中的 LIKE 關鍵字用於 `text` 資料類型之資料行間的比較，不過，如果 BLOB 類型中，資料大小大於 8K，則比較將會失敗。  
  
-   
  `ntext` 資料中的特殊字元可能會因為 BLOB 類型的比較限制而造成 SQLXML 4.0 的問題。 例如，用於 `<diffgr:before>` 類型之資料行的並行檢查中時，在 DiffGram 的 `ntext` 區塊中使用 "[Serializable]" 將會失敗，並顯示下列 SQLOLEDB 錯誤描述：  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  
