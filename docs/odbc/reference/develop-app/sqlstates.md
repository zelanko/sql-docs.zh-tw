---
description: SQLSTATE
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
ms.openlocfilehash: b32a965779da1669452e9361e38723e29cfb11ca
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476390"
---
# <a name="sqlstates"></a>SQLSTATE
SQLSTATEs 會提供警告或錯誤原因的詳細資訊。 本手冊中的 SQLSTATEs 是以 ISO/IEF CLI 規格中的方式為基礎，但以 IM 開頭的 SQLSTATEs 是 ODBC 專用的。  
  
 與傳回碼不同的是，此手冊中的 SQLSTATEs 是指導方針，而驅動程式不需要傳回它們。 因此，雖然驅動程式應該針對它們能夠偵測的任何錯誤或警告傳回適當的 SQLSTATE，但應用程式不一定會在這種情況下算出。 這種情況的原因有兩個：  
  
-   **不完整性** 雖然此手冊會列出大量的錯誤和警告，以及這些錯誤和警告的可能原因，但它並不完整，而且可能永遠不會有;驅動程式的執行方式變化太多了。 任何指定的驅動程式可能不會傳回此手冊中列出的所有 SQLSTATEs，而且可能會傳回此手冊未列出的 SQLSTATEs。  
  
-   **複雜度** 某些資料庫引擎（特別是關係資料庫引擎）會傳回無數的錯誤和警告。 這類引擎的驅動程式不太可能會將這些錯誤和警告對應至 SQLSTATEs，因為涉及的工作、對應的 inexactness、產生的程式碼大小，以及產生的程式碼的低值，這通常會傳回在執行時間永遠不會發生的程式設計錯誤。 因此，驅動程式應盡可能地將錯誤和警告視為合理，並請務必對應這些錯誤和警告，也就是應用程式邏輯可能依據的 SQLSTATE 01004 (資料遭截斷) 。  
  
 由於 SQLSTATEs 不會可靠地傳回，因此大部分的應用程式只會向使用者顯示其相關聯的診斷訊息，這通常是針對發生的特定錯誤或警告量身打造的，以及原生錯誤碼。 這樣做很少會遺失任何功能，因為應用程式還是無法在大部分的 SQLSTATEs 上以程式設計邏輯為基礎。 例如，假設 **SQLExecDirect** 傳回 SQLSTATE 42000 (語法錯誤或存取違規) 。 如果導致此錯誤的 SQL 語句是由應用程式硬式編碼或建立的，則這會是程式設計錯誤，而且必須修正程式碼。 如果使用者輸入 SQL 語句，這是使用者錯誤，而且應用程式已藉由通知使用者問題完成所有的工作。  
  
 當應用程式在 SQLSTATEs 上進行基本程式設計邏輯時，應該準備好讓 SQLSTATE 不被傳回，或傳回不同的 SQLSTATE。 確切傳回的 SQLSTATEs，只能以許多驅動程式的經驗為基礎。 不過，一般的指導方針是，SQLSTATEs 驅動程式或驅動程式管理員所發生的錯誤，而不是資料來源，則更可能可靠地傳回。 例如，大部分的驅動程式可能會傳回 SQLSTATE HYC00 (未) 執行的選用功能，但較少的驅動程式可能會傳回 SQLSTATE 42021 (資料行已存在) 。  
  
 下列 SQLSTATEs 會指出執行階段錯誤或警告，並且適合用來做為程式設計邏輯的基礎。 但是，並不保證所有驅動程式都會傳回它們。  
  
-   01004 (截斷的資料)   
  
-   01S02 (選項值已變更)   
  
-   已取消 HY008 (操作)   
  
-   HYC00 (未) 執行的選用功能  
  
-   HYT00 (Timeout 過期)   
  
 SQLSTATE HYC00 (未實) 的選擇性功能特別重要，因為它是應用程式可以用來判斷驅動程式是否支援特定語句或連接屬性的唯一方式。  
  
 如需完整的 SQLSTATEs 清單以及函式傳回它們的方式，請參閱 [附錄 a： ODBC 錯誤碼](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)。 如需每個函式可能傳回特定 SQLSTATE 之條件的詳細說明，請參閱該函數。
