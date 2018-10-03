---
title: 建立使用者定義階層 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- user-defined hierarchies [Analysis Services]
ms.assetid: 16715b85-0630-4a8e-99b0-c0d213cade26
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7cbef7b6adae6c8650b80b8c91bfd1357dde0541
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48218558"
---
# <a name="create-user-defined-hierarchies"></a>建立使用者定義階層
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可讓您建立使用者定義階層。 階層是以屬性為基礎的一組層級。 例如，時間階層可能包含年、季、月、週和日等層級。 在某些階層中，每個成員屬性都會唯一隱含上面的成員屬性。 這種階層有時稱為自然階層。 使用者可以使用階層來瀏覽 Cube 資料。 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，使用 [維度設計師] 中的 [階層] 窗格來定義階層。  
  
 建立使用者定義階層時，該階層可能會變成「不完全」。 在不完全階層中，至少一個成員的邏輯父成員不在成員的上一層級內。 如果您有不完全階層，有些設定可以控制是否可以看到遺漏的成員，以及如何顯示遺漏的成員。 如需詳細資訊，請參閱 [不完全階層](user-defined-hierarchies-ragged-hierarchies.md)。  
  
> [!NOTE]  
>  如需與使用者定義階層的設計和組態相關之效能問題的詳細資訊，請參閱 [SQL Server 2005 Analysis Services Performance Guide](http://go.microsoft.com/fwlink/?LinkId=81621)(SQL Server 2005 Analysis Services 效能指南)。  
  
## <a name="see-also"></a>另請參閱  
 [使用者階層屬性](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)   
 [層級屬性&#91;Paved Over&#93;](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies-level-properties.md)   
 [父子式階層](parent-child-dimension.md)  
  
  
