---
title: 升級將使全文檢索搜尋使用預設執行個體層級、 非全域的斷詞工具和篩選 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- filters [Full-Text Search]
- word breakers [Full-Text Search]
ms.assetid: 93ee8fcb-d11c-49fa-8fac-51ed31a8f008
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d1e4bfcaf022207afd7822740af104d6b9dbff2e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031569"
---
# <a name="upgrading-will-cause-full-text-search-to-use-instance-level-not-global-word-breakers-and-filters-by-default"></a>升級預設會使全文檢索搜尋使用執行個體層級、非全域的斷詞工具和篩選
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供可於執行個體層級註冊新斷詞工具和篩選的方法。  
  
## <a name="component"></a>元件  
 全文檢索搜尋  
  
## <a name="description"></a>描述  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允許新斷詞工具和篩選的執行個體層級註冊。 這種執行個體層級註冊提供了執行個體之間的功能和安全性隔離。  
  
## <a name="corrective-action"></a>更正動作  
 升級之後，請使用 `sp_fulltext_service` 來設定服務屬性以及允許載入元件的 `load_os_resources`。 您必須執行下列項目：  
  
 `sp_fulltext_service 'load_os_resources', 1`  
  
## <a name="see-also"></a>另請參閱  
 [使用 Upgrade Advisor](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  