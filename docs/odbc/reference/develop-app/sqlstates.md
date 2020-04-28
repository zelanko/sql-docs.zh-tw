---
title: SQLSTATEs |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], sqlstates
- SQLSTATE [ODBC]
ms.assetid: f29fff2e-3d09-4a8c-a2f9-2059062cbebf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be4bca929b8d48c301c6e71917503387004a6ec5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299725"
---
# <a name="sqlstates"></a>SQLSTATE
SQLSTATEs 會提供警告或錯誤原因的詳細資訊。 本手冊中的 SQLSTATEs 是根據 ISO/IEF CLI 規格中所找到的，但以 IM 開頭的 SQLSTATEs 則是針對 ODBC 而定。  
  
 不同于傳回碼，此手冊中的 SQLSTATEs 是指導方針，而驅動程式不需要傳回它們。 因此，雖然驅動程式應該針對能夠偵測到的任何錯誤或警告傳回適當的 SQLSTATE，但應用程式不應該在此一律發生的情況下計算。 這種情況的原因有兩個：  
  
-   **不完整性**雖然此手冊會列出大量錯誤和警告，以及這些錯誤和警告的可能原因，但它並不完整，而且可能永遠不會是;驅動程式的執行方式只會改變太多。 任何指定的驅動程式可能不會傳回此手冊中列出的所有 SQLSTATEs，而且可能會傳回此手冊中未列出的 SQLSTATEs。  
  
-   **複雜度**某些資料庫引擎-特別是關係資料庫引擎-傳回成千上萬的錯誤和警告。 這類引擎的驅動程式不太可能將所有的錯誤和警告對應至 SQLSTATEs，因為涉及的工作、對應的 inexactness、產生的程式碼大小，以及所產生程式碼的低值，這通常會傳回執行時間絕對不會遇到的程式設計錯誤。 因此，驅動程式應該盡可能對應多個錯誤和警告，並務必對應應用程式邏輯可能所依據的錯誤和警告，例如 SQLSTATE 01004 （資料已截斷）。  
  
 由於 SQLSTATEs 不會可靠地傳回，因此大部分的應用程式只會向使用者顯示其相關的診斷訊息，這通常會針對發生的特定錯誤或警告而量身打造，以及原生錯誤碼。 這麼做並不會有任何功能遺失，因為應用程式在大部分的 SQLSTATEs 上都無法以程式設計邏輯為基礎。 例如，假設**SQLExecDirect**傳回 SQLSTATE 42000 （語法錯誤或存取違規）。 如果造成此錯誤的 SQL 語句是硬式編碼或由應用程式所建立，則這是程式設計錯誤，而且必須修正程式碼。 如果使用者輸入 SQL 語句，這就是使用者錯誤，而且應用程式已藉由通知使用者問題來完成所有動作。  
  
 當應用程式在 SQLSTATEs 上進行基礎程式設計邏輯時，應該準備好讓 SQLSTATE 不會傳回，或傳回不同的 SQLSTATE。 確切傳回的 SQLSTATEs，只會以許多驅動程式的經驗為基礎。 不過，一般的指導方針是針對驅動程式或驅動程式管理員中所發生的錯誤（相對於資料來源）的 SQLSTATEs 較可能可靠地傳回。 例如，大部分的驅動程式可能會傳回 SQLSTATE HYC00 （未執行的選擇性功能），而較少的驅動程式可能會傳回 SQLSTATE 42021 （資料行已經存在）。  
  
 下列 SQLSTATEs 會指出執行階段錯誤或警告，而且很適合用來做為程式設計邏輯的基礎。 不過，並不保證所有驅動程式都會傳回它們。  
  
-   01004（資料已遭截斷）  
  
-   01S02 （選項值已變更）  
  
-   HY008 （操作已取消）  
  
-   HYC00 （未執行的選擇性功能）  
  
-   HYT00 （超時時間已過期）  
  
 SQLSTATE HYC00 （未實作為選擇性功能）特別重要，因為它是應用程式可判斷驅動程式是否支援特定語句或連接屬性的唯一方法。  
  
 如需 SQLSTATEs 的完整清單，以及函式傳回的函式，請參閱[附錄 a： ODBC 錯誤碼](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)。 如需每個函數可能傳回特定 SQLSTATE 之條件的詳細說明，請參閱該函式。
