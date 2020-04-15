---
title: 繫結列以區塊游標 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- column-wise binding [ODBC]
- row-wise binding [ODBC]
- result sets [ODBC], binding columns
- cursors [ODBC], block
- binding columns [ODBC]
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 231beede-cdfa-4e28-8b10-2760b983250f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bc7e527658a7d6945921510de898c648075c41fc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284898"
---
# <a name="binding-columns-for-use-with-block-cursors"></a>繫結資料行以搭配使用區塊資料指標
由於塊游標返回多行,因此使用它們的應用程序必須將變數陣列綁定到每列,而不是單個變數。 這些陣列統稱為*行集緩衝區*。 以下是繫結兩種樣式:  
  
-   將陣列綁定到每列。 這稱為*按列綁定*,因為每個數據結構(陣列)都包含單個列的數據。  
  
-   定義一個結構來保存整個行的數據並綁定這些結構的陣列。 這稱為*行綁定*,因為每個數據結構都包含單個行的數據。  
  
 與應用程式將單個變數綁定到列一樣,它調用**SQLBindCol**將陣列綁定到列。 唯一的區別是傳遞的位址是數位位址,而不是單個變數位址。 應用程式設置SQL_BIND_BY_COLUMN語句屬性以指定它是使用按列綁定還是按行綁定。 是按列綁定還是按行綁定,很大程度上是應用程式首選項的問題。 行綁定可能更貼近應用程式的數據佈局,在這種情況下,它將提供更好的性能。  
  
 此章節包含下列主題。  
  
-   [列-威斯綁定](../../../odbc/reference/develop-app/column-wise-binding.md)  
  
-   [行-威斯綁定](../../../odbc/reference/develop-app/row-wise-binding.md)
