---
title: 語法組的自動比對 | Microsoft Docs
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
- IntelliSense [SQL Server], delimiter highlighting
- IntelliSense [SQL Server], syntax pair matching
ms.assetid: bfc54cda-bfd6-4545-a5b9-f9db2ae13769
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 263481d1fe499ef59257d6f9211e638fe6c0b159
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37266245"
---
# <a name="automatic-matching-of-syntax-pairs"></a>語法組的自動比對
  語法組的自動比對會提供有關必須成對編碼的語法元素是否正確配對的立即回應給您。 這就是 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器中的分隔符號比對、Analysis Services XMLA 查詢編輯器中的大括號比對，以及 MDX 和 DMX 編輯器中的括號比對。  
  
## <a name="database-engine-query-editor-delimiter-matching"></a>Database Engine 查詢編輯器的分隔符號比對  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器會比對可識別程式碼區塊界限的分隔符號。 比對是以兩種方式完成：  
  
-   當您完成輸入配對中的第二個分隔符號時，編輯器就會反白顯示配對中的兩個分隔符號。  
  
-   游標隨時都位於配對的其中一個分隔符號內，因此您可以使用 CTRL+] 鍵盤快速鍵來跳到對稱的分隔符號。  
  
### <a name="delimiter-pairs"></a>分隔符號組  
 自動分隔符號比對會辨識下列分隔符號集合：  
  
|開頭分隔符號|結束分隔符號|  
|--------------------|-----------------------|  
|**(**|**)**|  
|**BEGIN**|**END**|  
|**BEGIN TRY**|**END TRY**|  
|**BEGIN CATCH**|**END CATCH**|  
  
 自動分隔符號比對不會辨識括號識別碼 ([ObjectName]) 或引號識別碼 ("ObjectName") 的分隔符號。 配對比對不會比對字串常值 ('string') 的單引號分隔符號，因為色彩編碼已經提供字串是否已分隔的視覺指示。  
  
### <a name="delimiter-highlighting"></a>分隔符號反白顯示  
 比對會反白顯示一對分隔符號的開頭和結束元素。 這可讓您以視覺化方式識別程式碼區塊並檢查是否有不對稱的分隔符號組。  
  
 當您輸入完成配對的最後一個字母時，分隔符號就會反白顯示。 例如，在您先輸入 BEGIN 然後接著 END 的 BEGIN END 配對中，當您輸入 END 的最後一個字母時，反白顯示就會開啟。 您不需要輸入開頭分隔符號，後面接著結尾分隔符號，即可開啟反白顯示。 如果您先輸入 END，然後向上捲動指令碼並輸入 BEGIN，則當您輸入 BEGIN 的最後一個字母時，反白顯示就會開啟。 輸入的最後一個字母不需要是分隔符號中的結尾字母。 例如，您可能會將 BEGIN 拼錯為 BEIN。當您插入最後一個 G 時，BEGIN END 配對就會反白顯示。  
  
 分隔符號組會維持反白顯示，直到您移動游標為止。 當游標移動時，反白顯示就會關閉，即使新的游標位置維持在相同的分隔符號中也一樣。 您可以透過刪除並重新輸入任何一個配對成員的任何字母，重新開啟反白顯示。  
  
## <a name="analysis-services-xmla-query-editor-brace-matching"></a>Analysis Services XMLA 查詢編輯器的大括號比對  
 XMLA 查詢編輯器的大括號比對會透過反白顯示左右大括號，顯示您是否已關閉元素。 您也可以使用 CTRL+] 鍵盤快速鍵，從一個大括號跳至對稱的大括號。  
  
 XMLA 查詢編輯器會針對下列詞彙進行大括號比對：  
  
-   對稱的開始與結束標記。  
  
-   任何一對 "\<" 和 ">" 角括弧。  
  
-   註解的開始與結束。  
  
-   處理指示的開始與結束。  
  
-   CDATA 區塊的開始與結束。  
  
-   DTD 宣告的開始與結束。  
  
-   屬性上的開頭及結束引號。  
  
## <a name="mdx-and-dmx-editor-parenthesis-matching"></a>MDX 和 DMX 編輯器的括號比對  
 多維度運算式 (MDX) 和資料採礦運算式 (DMX) 編輯器會自動比對函數中的括號組。  
  
  
