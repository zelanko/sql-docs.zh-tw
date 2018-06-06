---
title: 資料類型支援 |Microsoft 文件
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
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- data types [ODBC], ODBC drivers
- ODBC drivers [ODBC], data types
ms.assetid: 782b4490-372b-4366-aad7-a486fb8a07c8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 820e48a17e397bc9046c8ca431677074e69b8cb2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="data-type-support"></a>資料類型支援
ODBC 驅動程式必須支援至少一個 SQL_CHAR 和 SQL_VARCHAR。 其他資料類型的支援取決於驅動程式或資料來源的 SQL 92 一致性層級。 應用程式應該呼叫**SQLGetTypeInfo**判斷驅動程式所支援的資料類型。  
  
 如需有關資料類型的詳細資訊，請參閱[附錄 d： 資料型別](../../../odbc/reference/appendixes/appendix-d-data-types.md)。
