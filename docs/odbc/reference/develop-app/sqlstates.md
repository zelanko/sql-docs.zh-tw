---
title: "Sqlstate |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], sqlstates
- SQLSTATE [ODBC]
ms.assetid: f29fff2e-3d09-4a8c-a2f9-2059062cbebf
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0c99959fac35ac1cd312ab3d434f607c3f256dd8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlstates"></a>SQLSTATE
Sqlstate 會提供警告或錯誤的原因的詳細的資訊。 雖然使用 IM 啟動這些 Sqlstate 特有 ODBC Sqlstate 本手冊中取決於 ISO/IEF CLI 規格中。  
  
 不同於的傳回碼，此手冊中的 Sqlstate 是指導方針，並傳回它們，不需要的驅動程式。 因此，雖然驅動程式應該會傳回適當的 SQLSTATE 的任何錯誤或警告他們將能夠偵測，應用程式應該不會計算上此一律發生。 這種情況的原因有兩個：  
  
-   **不完整**; 雖然這份手冊列出大量的錯誤與警告以及可能的原因，這些錯誤和警告，但是不完整，而且可能永遠不會實作驅動程式只要改變太多。 任何指定的驅動程式可能不會傳回 Sqlstate 的所有列於此手冊，並可能會傳回 Sqlstate 未列在本手冊。  
  
-   **複雜性**的某些資料庫引擎 — 尤其是關聯式資料庫引擎-傳回逐字數千個錯誤和警告。 這類引擎的驅動程式不太可能，所有這些錯誤，以及涉及 Sqlstate 警告，因為所需的時間，對應的 inexactness、 大型大小的產生的程式碼，以及產生的程式碼，通常會傳回程式設計的低值永遠不會在執行階段發生的錯誤。 因此，驅動程式應將對應所有錯誤和警告似乎很合理，並務必將這些錯誤和警告的應用程式邏輯上都對應可能而定，例如 SQLSTATE 01004 （資料已截斷）。  
  
 因為無法可靠地傳回 Sqlstate，大部分的應用程式只會顯示它們至使用者以及其相關聯的診斷訊息，這通常適合特定的錯誤或發生的警告，以及原生錯誤碼。 會有很少任何遺失的功能，這項作業，因為應用程式無法根據程式設計邏輯，大部分的 Sqlstate 嗎。 例如，假設**SQLExecDirect**傳回 SQLSTATE 42000 （語法錯誤或存取違規）。 如果導致此錯誤的 SQL 陳述式是硬式編碼或應用程式所建立，這是程式設計錯誤，而且需要修正程式碼。 如果使用者輸入的 SQL 陳述式，則這是使用者錯誤，而且應用程式所有通知問題的使用者就可以完成。  
  
 當應用程式執行 Sqlstate 的基礎程式設計邏輯時，它們應該準備不是要傳回的 SQLSTATE 或傳回不同的 SQLSTATE。 完全都可靠地傳回 Sqlstate 可以是只根據許多驅動程式的經驗。 不過，一般來說是驅動程式或驅動程式管理員，而不是資料來源，在發生錯誤的 Sqlstate 是更可靠地傳回。 例如，大多數的驅動程式可能會傳回 SQLSTATE HYC00 （選擇性功能未實作），雖然較少的驅動程式可能會傳回 SQLSTATE 42021 （資料行已經存在）。  
  
 下列的 Sqlstate 指出執行階段錯誤或警告，並就非常適合作為基礎的程式設計邏輯。 不過，沒有保證所有的驅動程式傳回它們。  
  
-   01004 （資料已截斷）  
  
-   01S02 （選項值已變更）  
  
-   HY008 （取消作業）  
  
-   HYC00 （未實作的選擇性功能）  
  
-   HYT00 （逾時過期）  
  
 SQLSTATE HYC00 （未實作的選擇性功能） 是特別重要，因為它是在其中應用程式可以判斷驅動程式是否支援特定的陳述式或連接屬性的唯一方式。  
  
 Sqlstate 和哪些函式會傳回它們的完整清單，請參閱[附錄 a: ODBC 錯誤碼](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)。 在每個函式可能會傳回特定的 SQLSTATE 的條件的詳細說明，請參閱該函式。

