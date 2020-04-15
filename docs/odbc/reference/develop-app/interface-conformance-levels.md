---
title: 介面一致性級別 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 2c470e54-0600-4b2b-b1f3-9885cb28a01a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fff555324746fcb92641126ddf11ea91ce5e3f89
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304598"
---
# <a name="interface-conformance-levels"></a>介面一致性層級
平平的目的是通知應用程式驅動程式中可以使用哪些功能。 基於函數的平配方案不能充分實現這一目標。 在 ODBC 3 中。*x*,驅動程式根據他們擁有的功能進行分類。 支援該功能可以包括支援該功能;它還可以包括支援描述符位、語句屬性 **、SQLGetInfo**傳回的資訊類型的「Y」值等。  
  
 為了簡化介面一致性的規範,ODBC 定義了三個一致性級別。 為了滿足特定的一致性級別,驅動程式必須滿足該符合性級別的所有要求。 與給定級別的一致性意味著與所有較低級別完全一致。  
  
 一致性級別並不總是整齊地劃分為對特定 ODBC 函數列表的支援,而是指定以下各節中列出的受支援的功能。 要支援某項功能,驅動程式必須支援對某些 ODBC 函數的部分或全部調用(有關詳細資訊,請參閱[函數一致性](../../../odbc/reference/develop-app/function-conformance.md))、設置某些屬性(請參閱[屬性一致性](../../../odbc/reference/develop-app/attribute-conformance.md))和某些描述符位(請參閱[描述符字段一致性](../../../odbc/reference/develop-app/descriptor-field-conformance.md))。  
  
 應用程式通過連接到數據源並調用**SQLGetInfo** SQL_ODBC_INTERFACE_CONFORMANCE 選項來發現驅動程式的介面一致性級別。  
  
 驅動程式可以自由地實現超出其聲明完全一致性的級別。 應用程式透過呼叫**SQLGet 函數**(確定存在哪些 ODBC 函數)和**SQLGetInfo(** 以查詢各種其他 ODBC 功能)來發現任何此類附加功能。  
  
 有三個 ODBC 介面一致性級別:核心、級別 1 和級別 2。  
  
> [!NOTE]
>  這些符合性級別與 ODBC 2 *.x*中的同名 ODBC API 符合性級別的要求不同。 特別是,ODBC 2 *.x* API 符合性級別 1 所隱含的所有功能現在都是核心介面一致性級別的一部分。 因此,許多ODBC驅動程式可能會報告核心級介面的一致性。  
  
 此章節包含下列主題。  
  
-   [核心介面一致性](../../../odbc/reference/develop-app/core-interface-conformance.md)  
  
-   [層級 1 介面一致性](../../../odbc/reference/develop-app/level-1-interface-conformance.md)  
  
-   [層級 2 介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)  
  
-   [函式一致性](../../../odbc/reference/develop-app/function-conformance.md)  
  
-   [屬性一致性](../../../odbc/reference/develop-app/attribute-conformance.md)  
  
-   [描述項欄位一致性](../../../odbc/reference/develop-app/descriptor-field-conformance.md)
