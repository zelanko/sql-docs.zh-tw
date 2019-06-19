---
title: 介面一致性層級 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 74d4ceb4532ee09004f035958860833aef488aaa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62446685"
---
# <a name="interface-conformance-levels"></a>介面一致性層級
調節的目的是通知應用程式所提供功能給它的驅動程式。 函式為基礎的層級配置夠無法達到此目標。 在 ODBC 3。*x*，驅動程式就會歸類在根據他們擁有的功能。 支援的功能，才能包含支援此函式;它也可以包含支援所傳回的資訊類型的描述項欄位、 陳述式屬性、"Y"值**SQLGetInfo**，依此類推。  
  
 若要簡化的介面一致性的規格，ODBC 會定義三個一致性層級。 若要符合的特定一致性層級，驅動程式必須滿足所有的一致性層級的需求。 使用指定的層級的一致性表示所有層級較低的完整一致性。  
  
 一致性層級執行不一定分成整齊地支援特定的 ODBC 函數清單，但指定支援的功能，如下列各節中所列。 若要提供一項功能支援，驅動程式必須支援某些 ODBC 函數呼叫的部分或所有表單 (如需詳細資訊，請參閱[函式一致性](../../../odbc/reference/develop-app/function-conformance.md))，設定特定屬性 (請參閱[屬性一致性](../../../odbc/reference/develop-app/attribute-conformance.md))，以及特定描述項欄位 (請參閱 <<c8> [ 描述項欄位一致性](../../../odbc/reference/develop-app/descriptor-field-conformance.md))。  
  
 應用程式的驅動程式介面一致性層級會藉由探索連接到資料來源，然後呼叫**SQLGetInfo** SQL_ODBC_INTERFACE_CONFORMANCE 選項。  
  
 驅動程式可自行實作他們所宣告完整的一致性層級以外的功能。 應用程式探索任何這類額外的功能，藉由呼叫**SQLGetFunctions** （若要判斷哪些 ODBC 函式存在） 並**SQLGetInfo** （若要查詢各種其他的 ODBC 功能）。  
  
 有三個 ODBC 介面一致性層級：Core、 層級 1 和層級 2。  
  
> [!NOTE]
>  這些一致性層級比 ODBC 2 中的相同名稱的 ODBC API 的一致性層級有不同的需求 *.x*。 ODBC 2 的所有功能特別的是，都隱含 *.x* API 一致性層級 1 現在是核心介面一致性層級的一部分。 如此一來，許多 ODBC 驅動程式可能會報告層級的核心介面一致性。  
  
 此章節包含下列主題。  
  
-   [核心介面一致性](../../../odbc/reference/develop-app/core-interface-conformance.md)  
  
-   [層級 1 介面一致性](../../../odbc/reference/develop-app/level-1-interface-conformance.md)  
  
-   [層級 2 介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)  
  
-   [函式一致性](../../../odbc/reference/develop-app/function-conformance.md)  
  
-   [屬性一致性](../../../odbc/reference/develop-app/attribute-conformance.md)  
  
-   [描述項欄位一致性](../../../odbc/reference/develop-app/descriptor-field-conformance.md)
