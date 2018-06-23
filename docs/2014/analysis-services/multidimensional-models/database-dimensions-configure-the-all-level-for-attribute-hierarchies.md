---
title: 設定屬性階層的 （全部） 層級 |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e61b7606ab4a7c2418294133ad7c4f3b03672df1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36145721"
---
# <a name="configure-the-all-level-for-attribute-hierarchies"></a>設定屬性階層的 (全部) 層級
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中，(全部) 層級是系統產生的選擇性層級。 它只包含一個成員，而這個成員的值是直屬層級中所有成員的值彙總。 此成員叫作全部成員。 它是系統產生的成員，不包含在維度資料表中。 因為 (全部) 層級中的成員是在階層頂端，所以該成員值是此階層中所有成員值的合併彙總。 全部成員通常是做為階層的預設成員。  
  
 屬性階層中的 （全部） 層級與否取決於`IsAggregatable`屬性設定的屬性和使用者定義階層中的 （全部） 層級是否存在相依於`IsAggregatable`屬性的最高的層級的屬性使用者定義階層。 如果 `IsAggregatable` 屬性設為 `True`，則 (全部) 層級會存在。 如果 `IsAggregatable` 屬性設為 `False`，則階層沒有 (全部) 層級。  
  
## <a name="establishing-the-topmost-level"></a>建立最上層  
 如果 `IsAggregatable` 屬性設為階層中某層級之來源屬性上的 `False`，則可彙總層級不會出現在階層中的該層級上方。 不可彙總層級必須是任何階層的最上層，否則，它上方層級之來源屬性的 `IsAggregatable` 屬性也必須設為 `False`。  
  
## <a name="all-member-and-all-level"></a>全部成員和 (全部) 層級  
 (全部) 層級的單一成員叫做全部成員。 `AttributeAllMemberName`維度屬性在維度中指定之屬性的全部成員名稱。 階層的 `AllMemberName` 屬性指定階層的全部成員名稱。  
  
## <a name="see-also"></a>另請參閱  
 [定義預設成員](attribute-properties-define-a-default-member.md)  
  
  