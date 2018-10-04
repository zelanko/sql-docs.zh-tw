---
title: 升級會使全文檢索搜尋使用預設執行個體層級、 非全域的斷詞工具和篩選 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- filters [Full-Text Search]
- word breakers [Full-Text Search]
ms.assetid: 93ee8fcb-d11c-49fa-8fac-51ed31a8f008
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d1974d81e36842f8c8d2c8ae70eceec26acb2dfe
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48175678"
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
 [使用升級建議程式](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
