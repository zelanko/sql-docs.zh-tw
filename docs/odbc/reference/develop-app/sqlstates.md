---
title: SQLSTATEs |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299725"
---
# <a name="sqlstates"></a>SQLSTATE
SQLSTAT 提供有關警告或錯誤原因的詳細資訊。 本手冊中的 SQLSTATE 基於 ISO/IEF CLI 規範中的 SQLSTAT,儘管以 IM 開頭的 SQLSTAT 特定於 ODBC。  
  
 與返回代碼不同,本手冊中的 SQLSTAT 是指南,並且不需要驅動程式來返回它們。 因此,雖然驅動程式應返回正確的 SQLSTATE,以查找它們能夠檢測到的任何錯誤或警告,但應用程式不應始終依賴這種情況。 造成這種情況的原因有兩個方面:  
  
-   **不要完整**儘管本手冊列出了大量錯誤和警告以及這些錯誤和警告的可能原因,但它不完整,可能永遠不會是;驅動程序實現差異太大。 任何給定的驅動程式可能不會返回本手冊中列出的所有 SQLSTATEs,並且可能會返回本手冊中未列出的 SQLSTAT。  
  
-   **複雜性**某些資料庫引擎(尤其是關係資料庫引擎)會返回數千個錯誤和警告。 由於所涉及的工作量、映射的不準確性、生成的代碼的大大小以及生成的代碼的較低值,此類引擎的驅動程式不太可能將所有這些錯誤和警告映射到 SQLSTATE,這些錯誤和警告通常返回在運行時不應遇到的程式設計錯誤。 因此,驅動程式應映射盡可能多的錯誤和警告,似乎合理,並確保映射應用程式邏輯可能基於的錯誤和警告,如 SQLSTATE 01004(數據截斷)。  
  
 由於 SQLStatEs 無法可靠地返回,因此大多數應用程式只是將它們與其關聯的診斷消息一起顯示給使用者,該消息通常針對發生的特定錯誤或警告以及本機錯誤代碼進行定製。 執行此操作時很少會丟失任何功能,因為應用程式無論如何都不能將程式設計邏輯基於大多數 SQLSTAT。 例如,假設**SQLExecDirect**傳回 SQLSTATE 42000(語法錯誤或存取衝突)。 如果導致此錯誤的 SQL 語句是硬編碼或由應用程式構建的,則這是一個程式設計錯誤,需要修復代碼。 如果使用者輸入 SQL 語句,則這是使用者錯誤,應用程式通過通知用戶問題,完成了所有可能的事情。  
  
 當應用程式對 SQLSTATEs 執行基本程式設計邏輯時,應為不返回 SQLSTATE 或返回其他 SQLSTATE 做好準備。 準確返回哪些 SQLSTAT 可以僅基於具有眾多驅動程式的經驗。 但是,一般準則是,與數據源相比,驅動程式或驅動程式管理器中發生的錯誤的 SQLSTAT 更有可能可靠地返回。 例如,大多數驅動程式可能返回 SQLSTATE HYC00(可選功能未實現),而返回 SQLSTATE 42021(已存在列)的驅動程式可能較少。  
  
 以下 SQLSTATE 指示執行時錯誤或警告,並且是建立程式設計邏輯的良好候選項。 但是,不能保證所有驅動程式都返回它們。  
  
-   01004 (資料截斷)  
  
-   01S02 (選項值已變更)  
  
-   HY008 (操作已取消)  
  
-   HYC00(未實作功能)  
  
-   HYT00(超時已過期)  
  
 SQLSTATE HYC00(未實現可選功能)特別重要,因為它是應用程式確定驅動程式是否支援特定語句或連接屬性的唯一方法。  
  
 有關 SQLSTAT 的完整清單以及傳回哪些函數,請參閱附錄[A:ODBC 錯誤代碼](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)。 有關每個函數可能返回特定 SQLSTATE 的條件的詳細說明,請參閱該函數。
