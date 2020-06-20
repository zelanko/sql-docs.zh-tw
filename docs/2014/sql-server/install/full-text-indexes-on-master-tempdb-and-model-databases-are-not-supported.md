---
title: 不支援 master、tempdb 和 model 資料庫的全文檢索索引 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes
ms.assetid: f7992965-42c1-4eb8-a7fb-afb38b67c740
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: fbd5e3133ed87fed9bdaf6d668df62c6471df766
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85012460"
---
# <a name="full-text-indexes-on-master-tempdb-and-model-databases-are-not-supported"></a>不支援 master、tempdb 和 model 資料庫的全文檢索索引
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允許在任何系統資料庫上使用全文檢索索引。  
  
## <a name="description"></a>描述  
 在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 中，master、tempdb 和 model 資料庫都支援全文檢索索引。  
  
 在升級期間，master、tempdb 和 model 資料庫中的任何全文檢索目錄都會移除。  
  
## <a name="see-also"></a>另請參閱  
 [使用升級建議程式](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
