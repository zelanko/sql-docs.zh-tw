---
title: 支援的平行存取模型（Visual FoxPro ODBC Driver） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], concurrency
- concurrency models [ODBC]
- FoxPro ODBC driver [ODBC], concurrency
ms.assetid: c39ed963-3af1-4888-8631-6083692ddcd7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 253a6dd86f6dc974d53dd151636bb8b8132e4d02
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307714"
---
# <a name="supported-concurrency-model-visual-foxpro-odbc-driver"></a>支援的並行存取模型 (Visual FoxPro ODBC Driver)
Visual FoxPro ODBC 驅動程式支援*唯讀的並行*存取。 您的應用程式可以使用 SQL_CONCUR_READ_ONLY 的 SQL_CONCURRENCY 選項來呼叫[SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) 。  
  
 如需詳細資訊，請參閱 ODBC 程式設計[人員參考](../../odbc/reference/odbc-programmer-s-reference.md)。  
  
## <a name="read-only-concurrency"></a>唯讀平行存取  
 無法更新資料指標。  
  
## <a name="row-versioning"></a>資料列版本設定  
 實質上是時間戳記支援，在更新時會比較資料列版本。
