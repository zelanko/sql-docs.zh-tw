---
description: 資料指標的類型 (ADO)
title: " (ADO) 的資料指標類型 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], types
ms.assetid: 7cc01544-e814-403b-bbfe-a2750bf921bd
author: rothja
ms.author: jroth
ms.openlocfilehash: adeaef5251ef5e9ebbc1e6b792f2647d3fcea250
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979309"
---
# <a name="types-of-cursors-ado"></a>資料指標的類型 (ADO)
一般來說，您的應用程式應該使用最簡單的資料指標，以提供必要的資料存取。 除了基本概念之外，每個額外的資料指標特性 (順向、唯讀、靜態、滾動、未緩衝) 具有用戶端記憶體、網路負載或效能的價格。 在許多情況下，預設資料指標選項會產生比您的應用程式實際需要更複雜的資料指標。  
  
 您選擇的資料指標類型，取決於您的應用程式如何使用結果集，以及數個設計考慮，包括結果集的大小、可能使用的資料百分比、資料變更的敏感度，以及應用程式效能需求。  
  
 在最基本的情況下，您的資料指標選擇取決於您是否需要變更或單純地查看資料：  
  
-   如果您只需要滾動一組結果，而不是變更資料，請使用順 [向](../../../ado/guide/data/forward-only-cursors.md) 或 [靜態](../../../ado/guide/data/static-cursors.md) 資料指標。  
  
-   如果您有大型結果集，而且只需要選取幾個資料列，請使用索引 [鍵集](../../../ado/guide/data/keyset-cursors.md) 資料指標。  
  
-   如果您想要同步處理所有並行使用者最近新增、變更和刪除的結果集，請使用 [動態](../../../ado/guide/data/dynamic-cursors.md) 資料指標。  
  
 雖然每個資料指標類型看起來都是相異的，但請記住，這些資料指標類型不會像是重迭特性和選項的結果那麼多。  
  
 此章節包含下列主題。  
  
-   [順向資料指標](../../../ado/guide/data/forward-only-cursors.md)  
  
-   [靜態資料指標](../../../ado/guide/data/static-cursors.md)  
  
-   [索引鍵集資料指標](../../../ado/guide/data/keyset-cursors.md)  
  
-   [動態資料指標](../../../ado/guide/data/dynamic-cursors.md)  
  
## <a name="see-also"></a>另請參閱  
 [順向資料指標](../../../ado/guide/data/forward-only-cursors.md)   
 [靜態資料指標](../../../ado/guide/data/static-cursors.md)   
 [索引鍵集資料指標](../../../ado/guide/data/keyset-cursors.md)   
 [動態資料指標](../../../ado/guide/data/dynamic-cursors.md)
