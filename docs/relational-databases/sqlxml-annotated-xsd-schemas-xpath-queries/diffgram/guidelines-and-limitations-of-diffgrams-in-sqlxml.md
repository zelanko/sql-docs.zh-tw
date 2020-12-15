---
description: 在 SQLXML 中的 DiffGrams 指導方針和限制
title: 在 SQLXML 中的 DiffGrams 指導方針和限制
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
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f5d9cbcd08d41f4ce134a663fdcc1cf1bd1c3298
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97414984"
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>在 SQLXML 中的 DiffGrams 指導方針和限制
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  搭配 SQLXML 4.0 使用 DiffGrams 時，請記住以下事項：  
  
-   使用 Diffgram 時，不應在區塊中使用二進位大型物件 (BLOB) 類型，例如 **text/Ntext** 和 images **\<diffgr:before>** ，因為這會包含它們以便在並行控制中使用。 這可能會因為 BLOB 類型的比較限制而造成 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的問題。 例如，WHERE 子句中使用 LIKE 關鍵字來比較 **text** 資料類型的資料行;但是，如果 BLOB 類型的資料大小大於8K，比較將會失敗。  
  
-   **Ntext** 資料中的特殊字元可能會因為 BLOB 類型的比較限制而造成 SQLXML 4.0 的問題。 例如，使用 **\<diffgr:before>** 在 DiffGram 的資料行的並行檢查中時，在 DiffGram 的區塊中使用 "[Serializable]" 將會失敗，並出現下列 SQLOLEDB 錯誤描述：  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  
