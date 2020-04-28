---
title: 資料類型支援 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- data types [ODBC], ODBC drivers
- ODBC drivers [ODBC], data types
ms.assetid: 782b4490-372b-4366-aad7-a486fb8a07c8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3abfe85ee32fb9ff4a8499c9949c0685563fec70
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81284425"
---
# <a name="data-type-support"></a>資料類型支援
ODBC 驅動程式必須至少支援其中一個 SQL_CHAR 和 SQL_VARCHAR。 其他資料類型的支援取決於驅動程式或資料來源的 SQL-92 一致性層級。 應用程式應該呼叫**SQLGetTypeInfo**來判斷驅動程式所支援的資料類型。  
  
 如需有關資料類型的詳細資訊，請參閱[附錄 D：資料類型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。
