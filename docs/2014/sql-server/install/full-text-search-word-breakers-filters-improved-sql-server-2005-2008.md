---
title: 在 SQL Server 2005 和 SQL Server 2008 大幅改進全文檢索搜尋的斷詞工具和篩選 |Microsoft Docs
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
- filters [Full-Text Search]
- word breakers [Full-Text Search]
ms.assetid: 8d06bda9-0bbf-4baa-b270-07b1c1f640eb
caps.latest.revision: 23
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6a28f0ba9c29be0366b34626fd1c28a7f98c404f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37315568"
---
# <a name="full-text-search-word-breakers-and-filters-significantly-improved-in-sql-server-2005-and-sql-server-2008"></a>SQL Server 2005 和 SQL Server 2008 大幅改進全文檢索搜尋斷詞工具和篩選功能
  斷詞工具與篩選已經大幅修改。 對斷詞工具做了進一步的改進，包括提高語言涵蓋範圍和可靠性。  
  
## <a name="description"></a>描述  
 為了改善功能和可靠性，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 全文檢索搜尋所使用的斷詞工具和篩選已經大幅修改。 在某些特定情況下，對斷詞工具所做的變更可能會影響部分資料的 Token 化方式。 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 中建立的 Token 可能與先前在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 或 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中建立的 Token 不同。  
  
 如需斷詞工具的資訊，請參閱[設定和管理的斷詞工具與字幹分析器搜尋](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)。  
  
## <a name="see-also"></a>另請參閱  
 [使用升級建議程式](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
