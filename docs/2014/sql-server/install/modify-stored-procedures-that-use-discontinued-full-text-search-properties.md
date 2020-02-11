---
title: 修改使用已停止全文檢索搜尋屬性的預存程式 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- discontinued properties [Full-Text Search]
- stored procedures [Full-Text Search]
ms.assetid: 8d9392d9-a9ba-4378-84e4-59f516b67ddb
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5204b27fb4745f8005a328dc62503f7db418387d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "66093844"
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
  
  
