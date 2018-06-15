---
title: 描述元 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC]
- descriptors [ODBC], about descriptors
- descriptor handles [ODBC]
- handles [ODBC], descriptor
ms.assetid: ef2cbb93-cd00-40f8-b1d2-5f5723a991aa
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e02316233f7e0c9722da90f4c2562282ce19bce9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32908813"
---
# <a name="descriptors"></a>描述元
描述項處理是指資料結構，可保存資料行或動態參數的相關資訊。  
  
 ODBC 函數在資料行和參數的資料上運作以隱含方式的設定，和擷取的描述項欄位。 例如，當**SQLBindCol**呼叫來繫結資料行的資料，它會設定完整地描述繫結的描述項欄位。 當**SQLColAttribute**呼叫來描述資料行的資料，它會傳回描述項欄位中儲存的資料。  
  
 呼叫 ODBC 函數的應用程式不需要與本身具有描述元。 任何資料庫作業不需要應用程式取得描述元的直接存取。 不過，對於某些應用程式，描述元的直接存取可簡化許多作業。 例如，直接存取描述元提供重新繫結資料行資料，可能會比呼叫更有效率的方式**SQLBindCol**一次。  
  
> [!NOTE]  
>  未定義的描述元的實體表示法。 應用程式獲得只是藉由呼叫 ODBC 函數具有描述元控制代碼操作其欄位的描述元的直接存取。  
  
 此章節包含下列主題。  
  
-   [描述項的類型](../../../odbc/reference/develop-app/types-of-descriptors.md)  
  
-   [描述項欄位](../../../odbc/reference/develop-app/descriptor-fields.md)  
  
-   [配置及釋放描述項](../../../odbc/reference/develop-app/allocating-and-freeing-descriptors.md)  
  
-   [取得並設定描述項欄位](../../../odbc/reference/develop-app/getting-and-setting-descriptor-fields.md)
