---
title: 設定屬性階層的（全部）層級 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- All members
- IsAggregatable property
- topmost levels [Analysis Services]
- (All) levels
- AttributeAllMemberName property
- levels [Analysis Services]
- members [Analysis Services], All
- AllMemberName property
ms.assetid: 0cb35e6f-b10f-483d-b893-78f6ca3979fd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 95e1693333bbc228e16d01646283d41138d0aaf0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66076001"
---
# <a name="configure-the-all-level-for-attribute-hierarchies"></a>設定屬性階層的 (全部) 層級
  在[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，（全部）層級是系統產生的選擇性層級。 它只包含一個成員，而這個成員的值是直屬層級中所有成員的值彙總。 此成員叫作全部成員。 它是系統產生的成員，不包含在維度資料表中。 因為 (全部) 層級中的成員是在階層頂端，所以該成員值是此階層中所有成員值的合併彙總。 全部成員通常是做為階層的預設成員。  
  
 (全部) 層級是否出現在屬性階層中，視該屬性的 `IsAggregatable` 屬性設定而定，(全部) 層級是否出現在使用者自訂階層中，視使用者自訂階層最上層之該屬性的 `IsAggregatable` 屬性而定。 如果 `IsAggregatable` 屬性設為 `True`，則 (全部) 層級會存在。 如果 `IsAggregatable` 屬性設為 `False`，則階層沒有 (全部) 層級。  
  
## <a name="establishing-the-topmost-level"></a>建立最上層  
 如果 `IsAggregatable` 屬性設為階層中某層級之來源屬性上的 `False`，則可彙總層級不會出現在階層中的該層級上方。 不可彙總層級必須是任何階層的最上層，否則，它上方層級之來源屬性的 `IsAggregatable` 屬性也必須設為 `False`。  
  
## <a name="all-member-and-all-level"></a>全部成員和 (全部) 層級  
 (全部) 層級的單一成員叫做全部成員。 維度`AttributeAllMemberName`上的屬性會指定維度中屬性的所有成員名稱。 階層的 `AllMemberName` 屬性指定階層的全部成員名稱。  
  
## <a name="see-also"></a>另請參閱  
 [定義預設成員](attribute-properties-define-a-default-member.md)  
  
  
