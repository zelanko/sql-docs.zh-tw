---
title: 檢索書簽 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving bookmarks [ODBC]
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
ms.assetid: a34c8f09-b786-4835-a44b-b7294c970aff
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3d146b2fb9bfc0e7294709e971f1b6752dc99ab3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300068"
---
# <a name="retrieving-bookmarks"></a>擷取書籤
如果應用程式將使用書籤,則必須在準備或執行語句之前將SQL_ATTR_USE_BOOKMARKS語句屬性設置為SQL_UB_VARIABLE。 這是必需的,因為構建和維護書籤可能是一項昂貴的操作,因此只有在應用程式能夠很好地使用它們時才能啟用書籤。  
  
 書籤將作為結果集的第 0 列返回。 應用程式可以檢索它們的方法有三種:  
  
-   綁定結果集的列 0。 **SQLFetch**或**SQLFetchScroll**返回行集中每行的書籤以及其他綁定列的數據。  
  
-   調用**SQLSetPos**定位到行集中的行,然後為列 0 調用**SQLGetData。** 如果驅動程式支援書籤,它必須始終支援為列 0 調用**SQLGetData**的能力,即使它不允許應用程式在最後一個綁定列之前為其他列調用**SQLGetData。**  
  
-   呼叫**SQLBulk 操作**,*操作*參數設定為SQL_ADD,第 0 列綁定。 游標插入該行並返回綁定緩衝區中行的書籤。
