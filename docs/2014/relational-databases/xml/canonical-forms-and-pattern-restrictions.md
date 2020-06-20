---
title: 標準格式與模式限制 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- pattern restrictions
- canonical forms
ms.assetid: 088314ec-7d0b-4a05-8a33-f35da5bfe59c
author: rothja
ms.author: jroth
ms.openlocfilehash: 569e8c4a01ed1eb9ae26ea9e2f6d471b9aad9fe0
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059575"
---
# <a name="canonical-forms-and-pattern-restrictions"></a>標準格式與模式限制
  XSD 模式 Facet 允許簡單類型的語彙空間限制。 當在有一個以上的可能語彙表示法之類型上設置模式限制時，有些值可能會在驗證時造成非預期的行為。  
  
 因為這些值的語彙表示法並未儲存在資料庫中，就會發生此行為。 因此，當序列化為輸出時，這些值會轉換成其標準的表示法。 當文件包含一個值，而值的標準格式不符合其類型的模式限制時，如果使用者嘗試重新插入它，將會拒絕該文件。  
  
 為了避免此情形， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將會拒絕包含無法重新插入的值之 XML 文件，因為違反了其標準格式的模式限制。 例如，值 "33.000" 將不會針對具有 "33 **.0+" 模式限制之** xs:decimal\\所衍生的類型驗證。 雖然 "33.000" 符合此模式，但是標準格式 "33" 卻不符合。  
  
 因此，當您將模式 Facet 套用到衍生自下列基本類型的類型時，應該要特別小心：`boolean`、`decimal`、`float`、`double`、`dateTime`、`time`、`date`、`hexBinary` 和 `base64Binary`。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就會發出警告。  
  
 不精確的浮點值序列化具有類似的問題。 由於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用浮點序列化演算法，類似的值有可以共用相同的標準格式。 當序列化和重新插入浮點值時，它有可能變更其值。 在極少數的情況下，這可能會在重新插入時，產生違反下列任何 Facet 類型的值： **enumeration**、 **minInclusive**、 **minExclusive**、 **maxInclusive**或 **maxExclusive**。 為了避免此情形， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會拒絕從無法序列化和重新插入的 `xs:float` 或 `xs:double` 所衍生的任何類型值。  
  
## <a name="see-also"></a>另請參閱  
 [伺服器上 XML 結構描述集合的需求與限制](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
