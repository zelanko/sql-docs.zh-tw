---
title: 不允許在非保存計算資料行上的全文檢索索引 |Microsoft Docs
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
- full-text indexes
ms.assetid: cba737f7-b187-47d0-8458-23dc18d18aca
caps.latest.revision: 19
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2abb3dba12ec76a4acd5c94998fad69274495203
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37303618"
---
# <a name="full-text-indexes-on-nonpersisted-computed-columns-are-not-allowed"></a>不允許在非保存的計算資料行上使用全文檢索索引
  您不可在不具決定性且不精確的計算資料行上建立全文檢索索引。 這樣的資料行無法做為類型資料行或全文檢索索引鍵資料行。  
  
## <a name="description"></a>描述  
 在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 中，您可以使用不具決定性且不精確的計算資料行當做類型資料行或全文檢索索引鍵資料行，建立全文檢索索引。 但是，目前已不支援這項功能。 當您升級時，系統會停用較舊、不相容和不支援的全文檢索索引。  
  
## <a name="corrective-action"></a>更正動作  
 若要啟用這些全文檢索索引，請修改資料行定義，讓這些資料行具決定性且精確。  
  
## <a name="see-also"></a>另請參閱  
 [使用升級建議程式](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
