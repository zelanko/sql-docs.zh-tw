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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: da899e4dc47daff03c31277b3edd4d9c642b87cb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305289"
---
# <a name="cursors"></a>資料指標
應用程式會使用資料*指標*來提取資料。 資料指標與結果集不同：結果集是符合特定搜尋條件的一組資料列，而資料指標則是將這些資料列傳回給應用程式的軟體。 名稱*游標*套用至資料庫時，可能是源自電腦終端機上的閃爍游標。 就如同該資料指標指出螢幕上的目前位置，以及輸入的單字接下來，結果集的資料指標會指出結果集內的目前位置，以及下一次將傳回的資料列。  
  
 ODBC 中的資料指標模型是以內嵌 SQL 中的資料指標模型為基礎。 這些模型之間有一項明顯的差異，就是資料指標的開啟方式。 在內嵌 SQL 中，必須先明確宣告並開啟資料指標，才能使用它。 在 ODBC 中，當執行建立結果集的語句時，會隱含地開啟資料指標。 當資料指標開啟時，它會位於結果集的第一個資料列之前。 在內嵌 SQL 和 ODBC 中，資料指標必須在應用程式完成使用之後關閉。  
  
 不同的資料指標具有不同的特性。 最常見的資料指標類型（稱為順向資料*指標）* 只能透過結果集向前移動。 若要回到前一個資料列，應用程式必須關閉並重新開啟資料指標，然後從結果集的開頭讀取資料列，直到到達必要的資料列為止。 順向資料指標提供快速的機制，讓單一階段通過結果集。  
  
 順向資料指標較不適用於以螢幕為基礎的應用程式，使用者可以在其中向前和向後流覽資料。 這類應用程式可以藉由讀取結果集一次來使用順向資料指標、在本機快取資料，以及自行執行滾動。 不過，這只適用于少量的資料。 較佳的解決方法是使用可滾動的資料*指標，* 它會提供對結果集的隨機存取。 這類應用程式也可以使用所謂的*區塊資料指標*，一次提取一個以上的資料列來增加效能。 如需區塊資料指標的詳細資訊，請參閱[使用區塊資料指標](../../../odbc/reference/develop-app/using-block-cursors.md)。  
  
 順向資料指標是 ODBC 中的預設資料指標類型，會在下列各節中討論。 如需區塊資料指標和可滾動資料指標的詳細資訊，請參閱[區塊資料指標](../../../odbc/reference/develop-app/block-cursors.md)和可[滾動游標](../../../odbc/reference/develop-app/scrollable-cursors.md)。  
  
> [!IMPORTANT]  
>  藉由明確呼叫**SQLEndTran**或在自動認可模式中操作來認可或回復交易，會導致某些資料來源關閉連接上所有語句上的所有資料指標。 如需詳細資訊，請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函數描述中的 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 屬性。
