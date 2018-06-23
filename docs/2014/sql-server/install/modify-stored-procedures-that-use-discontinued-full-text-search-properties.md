---
title: 修改使用停止的全文檢索搜尋屬性的預存程序 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- discontinued properties [Full-Text Search]
- stored procedures [Full-Text Search]
ms.assetid: 8d9392d9-a9ba-4378-84e4-59f516b67ddb
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 027fb2a7148dc0948c519836f30c8931d61f610b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034094"
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
 [使用 Upgrade Advisor](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  