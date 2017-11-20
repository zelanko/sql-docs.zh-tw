---
title: "資料指標 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- forward-only cursors [ODBC]
- scrollable cursors [ODBC]
- cursors [ODBC], about cursors
- cursors [ODBC]
- fetches [ODBC], cursors
- result sets [ODBC], fetching
- block cursors [ODBC]
ms.assetid: 0b114352-3c63-4d33-9220-182ede90e4aa
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 55a10004936cc2333eca14fd66123b929e8b9e5c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="cursors"></a>資料指標
應用程式提取資料與*游標*。 資料指標是不同的結果集： 結果集的資料列集，顯示符合特定搜尋條件，而游標位於軟體的應用程式傳回的資料列。 名稱*資料指標，*套用至資料庫時，可能是來自終端機的電腦上閃爍的游標。 就像該資料指標會指出目前的位置，在螢幕上的具類型的文字會出現 下一步，結果集的資料指標會指出目前的位置，在結果集中，以及哪些資料列將會傳回下一步。  
  
 在 ODBC 中的資料指標模型根據在 embedded SQL 資料指標模型。 一個顯著的差異，這些模型之間是方法的資料指標開啟。 在內嵌的 SQL 中，資料指標必須明確宣告，且開啟才能使用。 在 ODBC 中，開啟資料指標隱含地建立結果集的陳述式執行時。 資料指標開啟時，它會位於結果集的第一個資料列。 在內嵌 SQL 和 ODBC，應用程式使用它完成後，必須先關閉資料指標。  
  
 不同的資料指標具有不同的特性。 最常見的資料指標，它會呼叫類型*順向資料指標*只能在結果集中向前移動。 若要返回上一個資料列，應用程式必須關閉並重新開啟資料指標，然後從結果集，直到達到所需的資料列的開始讀取資料列。 順向資料指標提供快速的機制，讓單一通過結果集。  
  
 順向資料指標會是較不用於螢幕為基礎的應用程式，在使用者捲動向後和向前資料。 這類應用程式可以使用順向資料指標所讀取的結果集之後，快取在本機的資料，以及執行捲動本身。 不過，這也只適用於小量的資料。 更好的解決方案是使用*可捲動資料指標，*提供隨機存取的結果集。 這類應用程式也可以增加效能一次提取多個資料列所使用的名*區塊資料指標。* 如需區塊資料指標的詳細資訊，請參閱[使用區塊資料指標](../../../odbc/reference/develop-app/using-block-cursors.md)。  
  
 順向資料指標是在 ODBC 中的預設資料指標類型，以及下列各節中討論。 如需區塊資料指標和可捲動資料指標的詳細資訊，請參閱[區塊資料指標](../../../odbc/reference/develop-app/block-cursors.md)和[可捲動資料指標](../../../odbc/reference/develop-app/scrollable-cursors.md)。  
  
> [!IMPORTANT]  
>  認可或回復交易，藉由明確地呼叫**SQLEndTran**或根據在自動認可模式下操作，會導致某些資料來源，以關閉的連接上的所有陳述式的所有資料指標。 如需詳細資訊，請參閱中的 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 屬性[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函式描述。

