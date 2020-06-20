---
title: 全文檢索目錄名稱的長度限制為120個字元 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- full-text catalogs names
ms.assetid: 50633373-83f6-4ed9-99b9-71f92479a14f
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: fa9b06fa6fe4acd79782c19a8814357721e59c24
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85045206"
---
# <a name="length-of-full-text-catalog-names-restricted-to-120-characters"></a>全文檢索目錄名稱長度的限制是 120 個字元
  全文檢索目錄名稱的長度限制已經從舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 128 個字元，調降為 120 個字元。  
  
## <a name="description"></a>描述  
 此變更不會影響現有目錄名稱。不過，建立名稱超過 120 個字元之全文檢索目錄的指令碼會導致錯誤。 目錄名稱是用來產生對應至目錄的邏輯檔案名稱。  
  
## <a name="corrective-action"></a>更正動作  
 請修改建立全文檢索目錄的所有指令碼，確定它們將目錄名稱限制為 120 個字元。  
  
## <a name="see-also"></a>另請參閱  
 [使用升級建議程式](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
