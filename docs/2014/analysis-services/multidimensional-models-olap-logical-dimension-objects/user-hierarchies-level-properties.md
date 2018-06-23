---
title: 層級屬性 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- user hierarchies [Analysis Services]
- hierarchies [Analysis Services], user
ms.assetid: dabb7335-887b-442a-b67c-4901ba1242b7
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 38cb34a5cda2425870b73662707b1d1c2c2f3bdb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36136305"
---
# <a name="level-properties"></a>層級屬性 
  下表列出並描述使用者自訂階層中的層級屬性。  
  
|屬性|描述|  
|--------------|-----------------|  
|描述|包含層級的描述。|  
|HideMemberIf|指出是否應向用戶端應用程式隱藏層級中的成員，以及何時隱藏。 此屬性可以有下列的值：<br /><br /> 永不<br /> 永不隱藏成員。 這是預設值。<br /><br /> OnlyChildWithNoName<br /> 當成員是其父系的唯一子系，且成員的名稱為空白時，就會隱藏成員。<br /><br /> OnlyChildWithParentName<br /> 當成員是其父系的唯一子系，且成員與其父系有相同的名稱時，就會隱藏成員。<br /><br /> NoName<br /> 當成員的名稱為空白時，就會隱藏成員。<br /><br /> ParentName<br /> 當成員與其父系有相同的名稱時，就會隱藏成員。|  
|ID|包含層級的唯一識別碼 (ID)。|  
|[屬性]|包含層級的易記名稱。 依預設，層級與來源屬性有相同的名稱。|  
|SourceAttribute|包含作為層級基礎之來源屬性的名稱。|  
  
## <a name="see-also"></a>另請參閱  
 [使用者階層屬性](user-hierarchies-properties.md)  
  
  