---
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: eae0b81b3c55a4afe611cd8ed6fdbb495b498c61
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "75246602"
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>在 SQLXML 中的 DiffGrams 指導方針和限制
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  搭配 SQLXML 4.0 使用 DiffGrams 時，請記住以下事項：  
  
-   像是**text/Ntext**和 images 之類的** \<** 二進位大型物件（BLOB）類型不應在 diffgr 中使用：在使用 diffgram 時，在中>區塊，因為這會包含它們以在並行控制中使用。 這可能會因為 BLOB 類型的比較限制而造成 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的問題。 例如，WHERE 子句中會使用 LIKE 關鍵字來比較**text**資料類型的資料行;不過，如果 BLOB 類型的資料大小大於8K，比較將會失敗。  
  
-   **Ntext**資料中的特殊字元可能會因為 BLOB 類型的比較限制而造成 SQLXML 4.0 的問題。 例如，在** \<diffgr**中使用 "[Serializable]" 時>：在**DiffGram 類型的**資料行的並行檢查中使用時，會失敗，並出現下列 SQLOLEDB 錯誤描述：  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  
