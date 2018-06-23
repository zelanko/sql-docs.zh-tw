---
title: 設定快速剖析 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: dcd1dc09-6eaf-440b-9ce6-fef779ff794f
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 94f4fe123cb37e60e175ad39b932e61376e217b8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030820"
---
# <a name="set-fast-parse"></a>設定快速剖析
  使用快速剖析的來源或轉換，其每一個資料行都必須設定快速剖析屬性。 若要設定屬性，請使用「一般檔案」來源或「資料轉換」的進階編輯器。  
  
### <a name="to-set-fast-parse"></a>設定快速剖析  
  
1.  以滑鼠右鍵按一下 [一般檔案] 來源或 [資料轉換]，然後按一下 [顯示進階編輯器]。  
  
2.  按一下 **[進階編輯器]** 對話方塊中的 **[輸入與輸出屬性]** 索引標籤。  
  
3.  在 **[輸入及輸出]** 窗格中，按一下您要啟用快速剖析的資料行。  
  
4.  在 屬性 視窗中，依序展開**Custom Properties**  節點，並將其設定`FastParse`屬性`True`。  
  
5.  按一下 [確定] 。  
  
  