---
title: 描述元 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC]
- descriptors [ODBC], about descriptors
- descriptor handles [ODBC]
- handles [ODBC], descriptor
ms.assetid: ef2cbb93-cd00-40f8-b1d2-5f5723a991aa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f2138a5f8417fc9156c916719e96d707b9a29de9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68040015"
---
# <a name="descriptors"></a>描述項
描述項控制代碼是指資料結構，其中保存資料行或將動態參數的相關資訊。  
  
 ODBC 函數會隱含地在資料行和參數的資料上運作的設定，並擷取描述項欄位。 舉個例說，當**SQLBindCol**稱為資料行資料繫結，它會設定完整地描述繫結的描述項欄位。 當**SQLColAttribute**稱為來描述資料行的資料，它會傳回描述項欄位中儲存的資料。  
  
 呼叫 ODBC 函數的應用程式需要考慮本身描述元。 沒有資料庫作業需要的應用程式直接存取描述元。 不過，某些應用程式的描述元的直接存取可簡化許多作業。 比方說，直接存取描述項可用來重新繫結資料行資料，可能會比呼叫更有效率**SQLBindCol**一次。  
  
> [!NOTE]  
>  未定義的描述元的實體表示法。 應用程式獲得描述元的直接存取，只是藉由呼叫 ODBC 函數具有描述元控制代碼操作其欄位。  
  
 此章節包含下列主題。  
  
-   [描述項的類型](../../../odbc/reference/develop-app/types-of-descriptors.md)  
  
-   [描述項欄位](../../../odbc/reference/develop-app/descriptor-fields.md)  
  
-   [配置及釋放描述項](../../../odbc/reference/develop-app/allocating-and-freeing-descriptors.md)  
  
-   [取得並設定描述項欄位](../../../odbc/reference/develop-app/getting-and-setting-descriptor-fields.md)
