---
title: 取得一行資料 :微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305669"
---
# <a name="fetching-a-row-of-data"></a>擷取一列資料
要取得一行資料,應用程式呼叫**SQLFetch**。 **SQLFetch**可以使用任何類型的游標調用,但它僅向前移動行集游標。 **SQLFetch**將游標推進到下一行,並返回與**SQLBindCol**調用綁定的任何列的數據。 當游標到達結果集的末尾時 **,SQLFetch**將返回SQL_NO_DATA。 有關呼叫**SQLFetch**的範例,請參閱[使用 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)。  
  
 **SQLFetch**的實現方式正是特定於驅動程式的,但一般模式是驅動程式從數據源檢索任何綁定列的數據,根據綁定變數的類型進行轉換,並將轉換後的數據放在這些變數中。 如果驅動程式無法轉換任何資料 **,SQLFetch**將返回一個錯誤。 應用程式可以繼續提取行,但當前行的數據將丟失。 未綁定列的數據會發生什麼情況取決於驅動程式,但大多數驅動程序要麼檢索並丟棄它,要麼根本不檢索它。  
  
 驅動程式還設置已綁定的任何長度/指示器緩衝區的值。 如果列的資料值為 NULL,則驅動程式將相應的長度/ 指示器緩衝區設置為SQL_NULL_DATA。 如果資料值不是 NULL,驅動程式將長度/指示器緩衝區設置為轉換後數據的位元組長度。 如果無法確定此長度(有時對於由多個函數調用檢索的長數據的情況),驅動程式會將長度/指示器緩衝區設置為SQL_NO_TOTAL。 對於固定長度數據類型(如整數和日期結構),位元組長度是數據類型的大小。  
  
 對於變數長度數據(如字元和二進位資料),驅動程式根據綁定到列的緩衝區的位元組長度檢查轉換數據的位元長度;緩衝區的長度在**SQLBindCol**中的*緩衝區長度*參數中指定。 如果轉換數據的位元組長度大於緩衝區的位元組長度,驅動程式會截斷以放入緩衝區的數據,返回長度/指示器緩衝區中的未壓縮長度,返回SQL_SUCCESS_WITH_INFO,並將 SQLSTATE 01004(數據截斷)置於診斷中。 唯一的例外是,如果**SQLFetch**返回時截斷可變長度書籤,它返回 SQLSTATE 22001(字串數據,右截斷)。  
  
 固定長度數據永遠不會被截斷,因為驅動程式假定綁定緩衝區的大小是數據類型的大小。 數據截斷往往很少見,因為應用程式通常綁定足夠大的緩衝區來保存整個數據值;它確定元數據中的必要大小。 但是,應用程式可能會顯式綁定它知道太小的緩衝區。 例如,它可能會檢索和顯示零件說明的前 20 個字元或長文本列的前 100 個字元。  
  
 字元資料必須由驅動程式在返回到應用程式之前為null終止,即使已截斷。 返回的位元組長度中不包括空終止字元,但確實需要綁定緩衝區中的空格。 例如,假設應用程式使用由 ASCII 字元集中的字串資料組成的字串,驅動程式有 50 個字元的數據要返回,並且應用程式的緩衝區是 25 位元組長。 在應用程式的緩衝區中,驅動程式返回前 24 個字元,後跟一個空終止字元。 在長度/指示器緩衝區中,它返回位元組長度為50。  
  
 應用程式可以通過在執行創建結果集的語句之前設置SQL_ATTR_MAX_ROWS語句屬性來限制結果集中的行數。 例如,用於設置報表格式的應用程式中的預覽模式只需要足夠的數據來顯示報表的第一頁。 通過限制結果集的大小,此類功能將運行得更快。 此語句屬性旨在減少網路流量,並且可能不受所有驅動程序的支援。
