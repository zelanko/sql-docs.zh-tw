---
title: 複製描述符 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], copying
- copying descriptors [ODBC]
ms.assetid: 949a860d-6579-4218-882e-8c061688dd87
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2e2e5897afc3673a21396e256df04d25008c8cdf
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301667"
---
# <a name="copying-descriptors"></a>複製描述項
呼叫**SQLCopyDesc**函數將一個描述符號的欄位複製到另一個描述符號。 欄位只能複製到應用程式描述器或 IPD,但無法複製到 IRD。 可以從任何類型的描述符複製欄位。 僅複製為源和目標描述符定義的欄位。 **SQLCopyDesc**不會複製SQL_DESC_ALLOC_TYPE欄位,因為無法更改描述符的分配類型。 複製的欄位覆蓋現有欄位。  
  
 一個語句句柄上的 ARD 可以充當另一個語句句柄上的 APD。 這允許應用程式在表之間複製行,而無需在應用程式級別複製數據。 為此,描述表的提取行的行描述符將重新用作INSERT語句中參數的參數描述符。 SQL_MAX_CONCURRENT_ACTIVITIES資訊類型必須大於 1 才能成功此操作。
