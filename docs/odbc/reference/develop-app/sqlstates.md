---
title: SQLSTATEs | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8213c08e6844003d880129dda4b441a5592bbc86
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107339"
---
# <a name="sqlstates"></a>SQLSTATE
Sqlstate 會提供警告或錯誤的原因的詳細的資訊。 在本手冊中的 Sqlstate 根據在 ISO/IEF CLI 規格中，找到雖然開始 IM 這些 Sqlstate 特有 ODBC。  
  
 不同於傳回碼，在本手冊中的 Sqlstate 是指導方針，以及驅動程式不需要將它們傳回。 因此，雖然驅動程式應該會傳回適當的 SQLSTATE 的任何錯誤或警告的偵測，應用程式應該不會計算此一律出現。 這種情況的原因有兩個：  
  
-   **不完整**; 雖然這份手冊列出大量的錯誤和警告和可能的原因，這些錯誤和警告，但它不完整，而且可能也不會是驅動程式實作只要改變太多。 任何指定的驅動程式可能不會傳回 Sqlstate 的所有列在本手冊中，而且可能會傳回未列在本手冊的 Sqlstate。  
  
-   **複雜度**某些資料庫引擎-特別是關聯式資料庫引擎-傳回涉及數千個錯誤和警告。 這類引擎的驅動程式不太可能，所有這些錯誤和警告 Sqlstate，因為工作涉及，對應的 inexactness、 大型大小的產生的程式碼，以及產生的程式碼，通常會傳回程式設計的低值永遠不應該在執行階段發生的錯誤。 因此，驅動程式應該對應多個錯誤和警告起來似乎很合理，並務必將這些錯誤和警告的應用程式邏輯上對應可能而定，例如 SQLSTATE 01004 （資料已截斷）。  
  
 因為不會可靠地傳回 Sqlstate，大部分的應用程式只是其相關聯的診斷訊息，這通常適合特定的錯誤或發生的警告，以及使用者和原生錯誤程式碼顯示它們。 會有很少任何遺失的功能，在此情況下，因為應用程式無法根據程式設計邏輯，大部分的 Sqlstate 還是。 例如，假設**SQLExecDirect**傳回 SQLSTATE 42000 （語法錯誤或存取違規）。 如果 SQL 陳述式導致此錯誤是硬式編碼，或建置的應用程式，這是程式設計錯誤，而且需要修正程式碼。 如果使用者輸入的 SQL 陳述式，則這是使用者錯誤，而且應用程式完成所有便可能由通知問題的使用者。  
  
 當應用程式執行的程式設計邏輯基礎 Sqlstate 時，它們應該準備不是要傳回的 SQLSTATE 或傳回不同的 SQLSTATE。 完全其中可靠地傳回 Sqlstate 可以根據僅具有許多驅動程式的體驗。 不過，一般來說是驅動程式或驅動程式管理員，而不是資料來源中發生之錯誤的 Sqlstate 是更容易就能可靠地傳回。 例如，大部分的驅動程式可能會傳回 SQLSTATE HYC00 （未實作選擇性功能），而較少的驅動程式可能會傳回 SQLSTATE 42021 （資料行已存在）。  
  
 下列 Sqlstate 指出執行階段錯誤或警告，且是很好的候選項目作為基礎的程式設計邏輯。 不過，還有傳回它們，所有的驅動程式不保證。  
  
-   01004 （資料已截斷）  
  
-   01S02 （選項值已變更）  
  
-   HY008 （已取消的作業）  
  
-   HYC00 （未實作選擇性功能）  
  
-   HYT00 （逾時過期）  
  
 SQLSTATE HYC00 （未實作選擇性功能） 是特別重要，因為它是在其中應用程式可以判斷驅動程式是否支援特定的陳述式或連接屬性的唯一方法。  
  
 Sqlstate 和哪些函式會傳回它們的完整清單，請參閱[附錄 a:ODBC 錯誤碼](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)。 在其下每個函式可能會傳回特定的 SQLSTATE 條件的詳細說明，請參閱該函式。
