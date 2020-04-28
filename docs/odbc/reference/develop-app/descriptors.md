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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca8299daae744fb9398ed6ffc99c838ce8edff48
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305899"
---
# <a name="descriptors"></a>描述項
描述項控制碼是指保存資料行或動態參數相關資訊的資料結構。  
  
 在資料行和參數上操作的 ODBC 函數會隱含地設定和取出描述項欄位。 例如，呼叫**SQLBindCol**來系結資料行資料時，它會設定完整描述系結的描述項欄位。 當呼叫**SQLColAttribute**來描述資料行資料時，它會傳回儲存在描述項欄位中的資料。  
  
 呼叫 ODBC 函式的應用程式不需要與描述項本身顧慮。 任何資料庫作業都不需要應用程式取得描述元的直接存取權。 不過，對於某些應用程式，取得描述元的直接存取可簡化許多作業。 例如，直接存取描述元可提供重新系結資料行資料的方式，這比再次呼叫**SQLBindCol**更有效率。  
  
> [!NOTE]  
>  未定義描述元的實體表示。 應用程式只會藉由呼叫具有描述項控制碼的 ODBC 函式來操作其欄位，藉以取得描述項的直接存取權。  
  
 此章節包含下列主題。  
  
-   [描述項的類型](../../../odbc/reference/develop-app/types-of-descriptors.md)  
  
-   [描述項欄位](../../../odbc/reference/develop-app/descriptor-fields.md)  
  
-   [配置及釋放描述項](../../../odbc/reference/develop-app/allocating-and-freeing-descriptors.md)  
  
-   [取得並設定描述項欄位](../../../odbc/reference/develop-app/getting-and-setting-descriptor-fields.md)
