---
title: 檢索描述符位中的值 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: c05b180f-c2b0-437b-8d1c-ce7f4da93287
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 43467d19f3f2e576efa0402c4ba513e23da59390
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304319"
---
# <a name="retrieving-the-values-in-descriptor-fields"></a>擷取描述項欄位中的值
應用程式可以調用**SQLGetDescField**來獲取描述符記錄的單個字段。 **SQLGetDescField**使應用程式可以存取 ODBC 中定義的所有描述符欄位,以及驅動程式定義的欄位。  
  
 可以調用**SQLGetDescRec**來檢索影響列或參數數據的數據類型和存儲的多個描述符欄位的設置。
