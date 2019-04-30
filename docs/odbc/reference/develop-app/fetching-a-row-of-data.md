---
title: 正在擷取資料列 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFetch function [ODBC], fetching a row of data
- cursors [ODBC], fetching rows
- result sets [ODBC], fetching
- fetches [ODBC], row of data
ms.assetid: 16d4a380-0d83-456b-aeee-f10738944e86
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 012e454d03a0eb4ad16095353351d67e50d9586a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63061516"
---
# <a name="fetching-a-row-of-data"></a>擷取一列資料
若要擷取的資料列，應用程式會呼叫**SQLFetch**。 **SQLFetch**可以使用任何一種資料指標，呼叫，但它只會移動資料列集資料指標順向的方向。 **SQLFetch**游標前進到下一個資料列，並傳回已繫結呼叫的任何資料行的資料**SQLBindCol**。 當游標觸達結果結束設定，請**SQLFetch**傳回 sql_no_data 為止。 如需呼叫的範例**SQLFetch**，請參閱[使用 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)。  
  
 確切方式**SQLFetch**會實作驅動程式特有的但一般模式是以擷取資料的任何資料行繫結資料來源，將它根據繫結的變數的類型轉換，並設定驅動程式轉換中這些變數的詳細資料。 如果驅動程式無法將任何資料，轉換**SQLFetch**會傳回錯誤。 應用程式可以繼續提取資料列，但目前的資料列的資料都會遺失。 未繫結的資料行的資料會發生什麼情況取決於驅動程式，但大部分的驅動程式擷取並捨棄它或永遠不會進行擷取。  
  
 驅動程式也會設定都已繫結任何長度/指標緩衝區的值。 如果資料行的資料值為 NULL，則驅動程式會設定對應的長度/指標緩衝區為 SQL_NULL_DATA。 如果資料值不是 NULL，則驅動程式會設定為資料的位元組長度之長度/指標緩衝區轉換後。 如果無法判斷此長度，因為有時會與一個以上的函式呼叫所擷取的長資料的情況，則驅動程式會將長度/指標緩衝區設 SQL_NO_TOTAL。 固定長度資料類型，例如整數和日期結構的位元組長度會是資料類型的大小。  
  
 可變長度資料，例如字元和二進位資料，此驅動程式會檢查已轉換的資料，針對繫結至資料行緩衝區的位元組長度的位元組長度在指定的緩衝區長度*Columnsize*中的引數**SQLBindCol**。 如果已轉換資料的位元組長度大於緩衝區的位元組長度，驅動程式會截斷以符合緩衝區中的資料，則會傳回未截斷的長度，以長度/指標緩衝區中，會傳回 SQL_SUCCESS_WITH_INFO，並將 SQLSTATE 01004 （資料在診斷中截斷）。 唯一的例外是如果要在傳回時，截斷可變長度的書籤**SQLFetch**，它會傳回 SQLSTATE 22001 （字串資料，右邊已截斷）。  
  
 永遠不會截斷固定長度的資料，因為驅動程式會假設繫結的緩衝區大小，是資料類型的大小。 資料截斷可能相當罕見，因為應用程式通常會繫結的緩衝區不夠大，無法容納整個資料值;決定從中繼資料所需的大小。 不過，應用程式可能會明確繫結它知道得太小的緩衝區。 比方說，它可能會擷取並顯示組件描述的前 20 個字元或長的文字資料行的前 100 個字元。  
  
 字元資料必須以 null 結束驅動程式再將它傳回應用程式，即使它已被截斷。 Null 終止的字元不會包含在傳回的位元組長度，但不需要繫結的緩衝區中的空間。 比方說，假設應用程式會使用 ASCII 字元集中的字元資料所組成的字串、 驅動程式有 50 個字元的資料，若要傳回，而應用程式的緩衝區長度 25 個位元組。 在應用程式的緩衝區，驅動程式會傳回 null 結束字元為後面的第一次 24 個字元。 在長度/指標緩衝區，它會傳回位元組長度為 50。  
  
 應用程式可以限制結果集之前執行的陳述式，建立結果集，設定 SQL_ATTR_MAX_ROWS 陳述式屬性中的資料列數目。 比方說，在應用程式中用來格式化報表 [預覽] 模式必須足夠資料以顯示報表的第一頁。 藉由限制結果集的大小，此類功能的執行速度會更快。 此陳述式屬性是以減少網路流量，因此可能不支援所有的驅動程式。
