---
title: 介面一致性層級 |Microsoft 文件
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
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 2c470e54-0600-4b2b-b1f3-9885cb28a01a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 890684bf513b80cd484f7b15c75a04c38553513b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="interface-conformance-levels"></a>介面的一致性層級
調節的目的是通知哪些可用功能，從驅動程式的應用程式。 函式為基礎的撫平配置未充分達成這個目標。 在 ODBC 3。*x*，驅動程式就會歸類在根據他們擁有的功能。 支援的功能，可以包括支援函式。它也可以包含支援所傳回的資訊類型描述元欄位、 陳述式屬性、"Y"值**SQLGetInfo**，依此類推。  
  
 若要簡化介面一致性的規格，ODBC 會定義三個一致性層級。 若要符合特定的一致性層級，驅動程式必須滿足的所有需求的一致性層級。 使用給定的層級的一致性意味著所有層級較低的完整一致性。  
  
 一致性層級執行不一律分成完全支援特定的 ODBC 函數清單，但指定支援的功能，如下列各節中所列。 若要提供一項功能的支援，驅動程式必須支援某些 ODBC 函數呼叫的部分或所有表單 (如需詳細資訊，請參閱[函式一致性](../../../odbc/reference/develop-app/function-conformance.md))，設定特定屬性 (請參閱[屬性一致性](../../../odbc/reference/develop-app/attribute-conformance.md))，和特定描述項欄位 (請參閱[描述項欄位一致性](../../../odbc/reference/develop-app/descriptor-field-conformance.md))。  
  
 應用程式會探索連線至資料來源，然後呼叫的驅動程式介面一致性層級**SQLGetInfo** SQL_ODBC_INTERFACE_CONFORMANCE 選項。  
  
 驅動程式可用來實作超過他們所宣告完整的一致性層級的功能。 應用程式探索這類額外的功能，藉由呼叫**SQLGetFunctions** （若要判斷有哪些 ODBC 函數） 和**SQLGetInfo** （來查詢各種其他 ODBC 功能）。  
  
 有三個 ODBC 介面一致性層級： 核心、 層級 1 和層級 2。  
  
> [!NOTE]  
>  這些一致性層級比 ODBC 2 中的相同名稱的 ODBC API 的一致性層級有不同需求 *.x*。 特別是，所有功能都暗示 ODBC 2 *.x* API 的一致性層級 1 現在是核心介面的一致性層級的一部分。 如此一來，許多 ODBC 驅動程式可能會報告核心層級介面的一致性。  
  
 此章節包含下列主題。  
  
-   [核心介面一致性](../../../odbc/reference/develop-app/core-interface-conformance.md)  
  
-   [層級 1 介面一致性](../../../odbc/reference/develop-app/level-1-interface-conformance.md)  
  
-   [層級 2 介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)  
  
-   [函式一致性](../../../odbc/reference/develop-app/function-conformance.md)  
  
-   [屬性一致性](../../../odbc/reference/develop-app/attribute-conformance.md)  
  
-   [描述項欄位一致性](../../../odbc/reference/develop-app/descriptor-field-conformance.md)
