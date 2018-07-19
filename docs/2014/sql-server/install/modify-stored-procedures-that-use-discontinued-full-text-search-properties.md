---
title: 修改使用停止的全文檢索搜尋屬性的預存程序 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- discontinued properties [Full-Text Search]
- stored procedures [Full-Text Search]
ms.assetid: 8d9392d9-a9ba-4378-84e4-59f516b67ddb
caps.latest.revision: 20
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bd8fda3e9d1968d7dcc480931cf4ae8492bd4686
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37265804"
---
# <a name="modify-stored-procedures-that-use-discontinued-full-text-search-properties"></a>修改使用停止全文檢索搜尋屬性的預存程序
  若要確保您的預存程序會正確執行，您應該編輯現有的程序並移除已經被移除或取代的全文檢索相關屬性。  
  
## <a name="component"></a>元件  
 全文檢索搜尋  
  
## <a name="description"></a>描述  
 下列全文檢索搜尋相關的屬性和設定已移除。  
  
-   **DataTimeout**  
  
-   **ConnectTimeout**  
  
-   **Clean_up**  
  
-   **LogSize**  
  
 下列全文檢索搜尋相關的屬性和設定已移除或被取代：  
  
-   全文檢索目錄的「路徑」。 全文檢索目錄是不含系統中特定檔案路徑的邏輯物件。  
  
-   SP_FULLTEXT_DATABASE 中的 Enable/Disable 已經沒有任何作用，因為在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 中，資料庫永遠預設會啟用全文檢索搜尋。  
  
## <a name="corrective-action"></a>更正動作  
 請修改您的預存程序來移除這些屬性。  
  
## <a name="see-also"></a>另請參閱  
 [使用升級建議程式](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
