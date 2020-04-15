---
title: 描述符 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305899"
---
# <a name="descriptors"></a>描述項
描述符句柄是指保存有關列或動態參數的資訊的數據結構。  
  
 ODBC 函數對列和參數數據進行隱式設置和檢索描述符欄位。 例如,當調用**SQLBindCol**來綁定列數據時,它會設置完全描述綁定的描述符欄位。 當調用**SQLColAttribute**來描述列數據時,它將返回存儲在描述符欄位中的數據。  
  
 呼叫 ODBC 函數的應用程式不需要關注描述符本身。 沒有資料庫操作要求應用程式直接存取描述符。 但是,對於某些應用程式,直接訪問描述符可以簡化許多操作。 例如,直接訪問描述符提供了重新綁定列數據的方法,這比再次調用**SQLBindCol**更有效。  
  
> [!NOTE]  
>  描述符的物理表示形式未定義。 應用程式只能透過使用描述符句柄調用ODBC函數來直接存取描述符。  
  
 此章節包含下列主題。  
  
-   [描述項的類型](../../../odbc/reference/develop-app/types-of-descriptors.md)  
  
-   [描述項欄位](../../../odbc/reference/develop-app/descriptor-fields.md)  
  
-   [配置及釋放描述項](../../../odbc/reference/develop-app/allocating-and-freeing-descriptors.md)  
  
-   [取得並設定描述項欄位](../../../odbc/reference/develop-app/getting-and-setting-descriptor-fields.md)
