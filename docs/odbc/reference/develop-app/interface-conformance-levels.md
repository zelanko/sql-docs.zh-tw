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
ms.openlocfilehash: 185e68ed8d083e3ccfbab99369f6a778766a4c09
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138905"
---
# <a name="interface-conformance-levels"></a>介面一致性層級
「調節」的目的是要通知應用程式可從驅動程式使用哪些功能。 以函式為基礎的調節配置無法充分達成此目標。 在 ODBC 3 中。*x*，驅動程式是根據所擁有的功能來分類。 支援此功能包括支援函式;它也可以包含支援描述項欄位、語句屬性、 **SQLGetInfo**所傳回之資訊類型的 "Y" 值等等。  
  
 為了簡化介面一致性的規格，ODBC 定義了三個一致性層級。 為了符合特定的一致性層級，驅動程式必須滿足該一致性層級的所有需求。 具有給定層級的一致性意味著完全符合所有較低的層級。  
  
 一致性層級不一定會整齊地細分為特定 ODBC 函數清單的支援，但請指定下列各節所列的支援功能。 為了提供功能的支援，驅動程式必須支援某些 ODBC 函式的部分或所有形式呼叫（如需詳細資訊，請參閱[函數一致性](../../../odbc/reference/develop-app/function-conformance.md)）、設定特定屬性（請參閱[屬性一致性](../../../odbc/reference/develop-app/attribute-conformance.md)）和特定描述項欄位（請參閱[描述項欄位一致性](../../../odbc/reference/develop-app/descriptor-field-conformance.md)）。  
  
 應用程式會藉由連接到資料來源並使用 SQL_ODBC_INTERFACE_CONFORMANCE 選項呼叫**SQLGetInfo** ，來探索驅動程式的介面一致性層級。  
  
 驅動程式可自由地在其宣告完成一致性的層級以外執行功能。 應用程式會藉由呼叫**SQLGetFunctions** （判斷有哪些 odbc 函數存在）和**SQLGetInfo** （用來查詢各種其他 odbc 功能）來探索任何這類額外的功能。  
  
 ODBC 介面的一致性層級有三種：核心、層級1和層級2。  
  
> [!NOTE]
>  這些一致性層級與 ODBC 2.x 中相同名稱的 ODBC API 一致性層級具有不同的*需求。* 特別是，ODBC*2.X API 一致性*層級1所隱含的所有功能現在都是核心介面一致性層級的一部分。 因此，許多 ODBC 驅動程式可能會報告核心層級的介面一致性。  
  
 此章節包含下列主題。  
  
-   [核心介面一致性](../../../odbc/reference/develop-app/core-interface-conformance.md)  
  
-   [層級 1 介面一致性](../../../odbc/reference/develop-app/level-1-interface-conformance.md)  
  
-   [層級 2 介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)  
  
-   [函式一致性](../../../odbc/reference/develop-app/function-conformance.md)  
  
-   [屬性一致性](../../../odbc/reference/develop-app/attribute-conformance.md)  
  
-   [描述項欄位一致性](../../../odbc/reference/develop-app/descriptor-field-conformance.md)
