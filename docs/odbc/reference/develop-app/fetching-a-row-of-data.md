---
title: 提取資料列 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a702f561b756d5305020df9f015d3ea4b444caa6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305669"
---
# <a name="fetching-a-row-of-data"></a>擷取一列資料
若要提取資料列，應用程式會呼叫**SQLFetch**。 **SQLFetch**可以使用任何一種資料指標來呼叫，但它只會將資料列集資料指標以順向方向移動。 **SQLFetch**會將游標前移至下一個資料列，並傳回與**SQLBindCol**的呼叫系結之任何資料行的資料。 當資料指標到達結果集的結尾時， **SQLFetch**會傳回 SQL_NO_DATA。 如需呼叫**SQLFetch**的範例，請參閱[使用 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)。  
  
 確切地說， **SQLFetch**是如何實作為驅動程式特有的，但是一般模式是讓驅動程式從資料來源抓取任何系結資料行的資料，根據系結變數的型別進行轉換，然後將轉換的資料放在這些變數中。 如果驅動程式無法轉換任何資料， **SQLFetch**會傳回錯誤。 應用程式可以繼續提取資料列，但目前資料列的資料遺失。 未系結資料行的資料會根據驅動程式而有所不同，但大部分的驅動程式都是取出並捨棄它，或是完全不抓取。  
  
 驅動程式也會設定已系結之任何長度/指標緩衝區的值。 如果資料行的資料值為 Null，驅動程式會將對應的長度/指標緩衝區設定為 SQL_Null_DATA。 如果資料值不是 Null，驅動程式會在轉換後將長度/指標緩衝區設定為數據的位元組長度。 如果無法判斷此長度，就像有時候會有多個函式呼叫所抓取的長資料的情況，驅動程式會將長度/指標緩衝區設定為 SQL_NO_TOTAL。 如果是固定長度的資料類型（例如整數和日期結構），位元組長度就是資料類型的大小。  
  
 對於可變長度的資料，例如字元和二進位資料，驅動程式會根據系結至資料行之緩衝區的位元組長度，檢查已轉換資料的位元組長度。緩衝區的長度是在**SQLBindCol**的*BufferLength*引數中指定。 如果轉換資料的位元組長度大於緩衝區的位元組長度，驅動程式會截斷資料以納入緩衝區，傳回長度/指標緩衝區中的 untruncated 長度，傳回 SQL_SUCCESS_WITH_INFO，並在診斷中將 SQLSTATE 01004 （資料截斷）。 唯一的例外是，如果**SQLFetch**傳回可變長度的書簽，這會傳回 SQLSTATE 22001 （字串資料，右邊已截斷）。  
  
 固定長度的資料永遠不會截斷，因為驅動程式會假設系結緩衝區的大小是資料類型的大小。 資料截斷往往很罕見，因為應用程式通常會系結夠大的緩衝區來容納整個資料值;它會判斷中繼資料所需的大小。 不過，應用程式可能會明確地系結它知道太小的緩衝區。 例如，它可能會抓取並顯示部分描述的前20個字元或長文字資料行的前100個字元。  
  
 驅動程式在將其傳回給應用程式之前，必須以 null 終止字元資料，即使已截斷也一樣。 Null 終止字元不會包含在傳回的位元組長度中，而是需要系結緩衝區中的空間。 例如，假設應用程式使用 ASCII 字元集中的字元資料所組成的字串，驅動程式會有50個字元的資料要傳回，而應用程式的緩衝區長度為25個位元組。 在應用程式的緩衝區中，驅動程式會傳回前24個字元，後面接著 null 終止字元。 在長度/指標緩衝區中，它會傳回位元組長度50。  
  
 應用程式可以在執行建立結果集的語句之前，先設定 SQL_ATTR_MAX_ROWS 語句屬性，以限制結果集中的資料列數目。 例如，用來格式化報表的應用程式中的預覽模式，只需要足夠的資料，就能顯示報表的第一頁。 藉由限制結果集的大小，這項功能的執行速度會更快。 這個語句屬性的目的是要減少網路流量，而且可能不會受到所有驅動程式的支援。
