---
title: 支援併發模型(可視化福克斯Pro ODBC驅動程式) |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307714"
---
# <a name="supported-concurrency-model-visual-foxpro-odbc-driver"></a>支援的並行存取模型 (Visual FoxPro ODBC Driver)
視覺化福斯Pro ODBC驅動程式支援*唯讀併發*。 您的應用程式可以使用SQL_CONCURRENCY選項 SQL_CONCUR_READ_ONLY調用[SQLSetStmtOption。](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md)  
  
 有關詳細資訊,請參閱[ODBC 程式者的參考](../../odbc/reference/odbc-programmer-s-reference.md)。  
  
## <a name="read-only-concurrency"></a>唯讀並發  
 無法更新游標。  
  
## <a name="row-versioning"></a>資料列版本設定  
 本質上是時間戳支援,其中行版本在更新時進行比較。
