---
title: 不支援在 master、 tempdb 和 model 資料庫上的全文檢索索引 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes
ms.assetid: f7992965-42c1-4eb8-a7fb-afb38b67c740
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f055640dbdbf4ece491b2d8552c1581b122faed3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63240631"
---
# <a name="full-text-indexes-on-master-tempdb-and-model-databases-are-not-supported"></a>不支援 master、tempdb 和 model 資料庫的全文檢索索引
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允許在任何系統資料庫上使用全文檢索索引。  
  
## <a name="description"></a>描述  
 在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 中，master、tempdb 和 model 資料庫都支援全文檢索索引。  
  
 在 master、 tempdb 和 model 資料庫中的任何全文檢索目錄會在升級期間移除。  
  
## <a name="see-also"></a>另請參閱  
 [使用升級建議程式](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
