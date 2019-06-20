---
title: 資料指標 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- forward-only cursors [ODBC]
- scrollable cursors [ODBC]
- cursors [ODBC], about cursors
- cursors [ODBC]
- fetches [ODBC], cursors
- result sets [ODBC], fetching
- block cursors [ODBC]
ms.assetid: 0b114352-3c63-4d33-9220-182ede90e4aa
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 91765f0572d8c880f7505948f7756b373fe28f62
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63042124"
---
# <a name="cursors"></a>資料指標
應用程式會擷取資料*游標*。 資料指標是不同的結果集：結果集是符合特定搜尋準則的資料列集，而游標位於應用程式會傳回這些資料列的軟體。 名稱*資料指標，* 套用至資料庫時，可能源自終端機的電腦上閃爍的游標。 就像該資料指標會指出目前的位置，在螢幕上輸入的文字會出現下一步，結果集的資料指標會指出結果集，接下來將會傳回哪些資料列中的目前位置。  
  
 ODBC 中的資料指標模型根據在 embedded SQL 資料指標模型。 一個顯著的差異，這些模型之間是方法的資料指標開啟。 在內嵌的 SQL 中，資料指標必須明確宣告並開啟才能使用。 在 ODBC 中，開啟資料指標隱含地建立結果集的陳述式執行時。 資料指標開啟時，它會位於結果集的第一個資料列。 在 embedded SQL 和 ODBC，應用程式使用它完成後，必須先關閉資料指標。  
  
 不同的資料指標具有不同的特性。 最常見類型的資料指標，也就所謂*順向資料指標，* 只能透過結果集向前移動。 若要回到上一個資料列，應用程式必須關閉和重新開啟資料指標，然後從結果集，直到它到達所需的資料列的開始讀取資料列。 順向資料指標提供快速的機制來進行單一通過結果集。  
  
 順向資料指標是較不用於螢幕為基礎的應用程式，在使用者捲動向後和向前資料。 這類應用程式可以使用順向資料指標讀取的結果集之後，快取在本機的資料，以及執行捲動本身。 不過，這也只適用於小量的資料。 更好的解決方案是使用*捲動資料指標，* 提供隨機存取的結果集。 這類應用程式也可以增加效能所擷取的資料的多個資料列一次使用稱為*區塊資料指標。* 如需區塊資料指標的詳細資訊，請參閱[使用區塊資料指標](../../../odbc/reference/develop-app/using-block-cursors.md)。  
  
 順向資料指標是在 ODBC 中的預設資料指標類型，以及下列各節所述。 如需區塊資料指標和可捲動資料指標的詳細資訊，請參閱 <<c0> [ 區塊資料指標](../../../odbc/reference/develop-app/block-cursors.md)並[可捲動資料指標](../../../odbc/reference/develop-app/scrollable-cursors.md)。  
  
> [!IMPORTANT]  
>  認可或回復交易，藉由明確呼叫**SQLEndTran**或藉由在自動認可模式中操作，導致某些資料來源，以關閉的連接上的所有陳述式的所有資料指標。 如需詳細資訊，請參閱中的 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 屬性[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函式描述。
