---
title: 設定屬性階層的 （全部） 層級 |Microsoft 文件
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 23b00a88c8abf80045a38d0b8cc5d0c695949b0b
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34021675"
---
# <a name="database-dimensions---configure-the-all-level-for-attribute-hierarchies"></a>資料庫維度-設定屬性階層的 （全部） 層級
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中，(全部) 層級是系統產生的選擇性層級。 它只包含一個成員，而這個成員的值是直屬層級中所有成員的值彙總。 此成員叫作全部成員。 它是系統產生的成員，不包含在維度資料表中。 因為 (全部) 層級中的成員是在階層頂端，所以該成員值是此階層中所有成員值的合併彙總。 全部成員通常是做為階層的預設成員。  
  
 (全部) 層級是否出現在屬性 (attribute) 階層中，視該屬性 (attribute) 的 **IsAggregatable** 屬性 (property) 設定而定，(全部) 層級是否出現在使用者定義的階層中，視使用者定義階層最上層之該屬性 (attribute) 的 **IsAggregatable** 屬性 (property) 而定。 如果 **IsAggregatable** 屬性設為 **True**，則 (全部) 層級會存在。 如果 **IsAggregatable** 屬性設為 **False**，則階層沒有 (全部) 層級。  
  
## <a name="establishing-the-topmost-level"></a>建立最上層  
 如果 **IsAggregatable** 屬性設為階層中某層級之來源屬性上的 **False** ，則可彙總層級不會出現在階層中的該層級上方。 不可彙總層級必須是任何階層的最上層，否則，它上方層級之來源屬性 (attribute) 的 **IsAggregatable** 屬性 (property) 也必須設為 **False**。  
  
## <a name="all-member-and-all-level"></a>全部成員和 (全部) 層級  
 (全部) 層級的單一成員叫做全部成員。 維度上的 **AttributeAllMemberName**屬性 (property)，指定維度中之屬性 (attribute) 的全部成員名稱。 階層的 **AllMemberName** 屬性指定階層的全部成員名稱。  
  
## <a name="see-also"></a>另請參閱  
 [定義預設成員](../../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md)  
  
  
