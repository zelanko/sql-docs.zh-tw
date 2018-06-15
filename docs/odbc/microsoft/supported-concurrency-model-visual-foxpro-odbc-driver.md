---
title: 支援並行存取模型 （Visual FoxPro ODBC 驅動程式） |Microsoft 文件
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
- Visual FoxPro ODBC driver [ODBC], concurrency
- concurrency models [ODBC]
- FoxPro ODBC driver [ODBC], concurrency
ms.assetid: c39ed963-3af1-4888-8631-6083692ddcd7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 43ce790a912c78df9a0ef63e2172e69274ebb199
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32902565"
---
# <a name="supported-concurrency-model-visual-foxpro-odbc-driver"></a>支援並行存取模型 （Visual FoxPro ODBC 驅動程式）
Visual FoxPro ODBC 驅動程式支援*唯讀並行*。 您的應用程式可以呼叫[SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) SQL_CONCUR_READ_ONLY 的 SQL_CONCURRENCY 選項。  
  
 如需詳細資訊，請參閱[ODBC 程式設計人員參考](../../odbc/reference/odbc-programmer-s-reference.md)。  
  
## <a name="read-only-concurrency"></a>唯讀並行存取  
 無法更新資料指標。  
  
## <a name="row-versioning"></a>資料列版本設定  
 基本上是時間戳記支援，在哪一個資料列版本會在更新時間比較。
