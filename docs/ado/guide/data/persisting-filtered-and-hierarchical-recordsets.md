---
title: 保存篩選與階層式資料錄集 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- filtered Recordset persistence [ADO]
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: d01aeb4d-4e43-450b-b3f2-0c27eaaf9f86
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 53e28fdfbc49b53c4927bbcc0d5a6a8dc44b3d6d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62913313"
---
# <a name="persisting-filtered-and-hierarchical-recordsets"></a>保存篩選過的階層式資料錄集
如果[篩選條件](../../../ado/reference/ado-api/filter-property.md)屬性實際上是針對**資料錄集**，儲存的資料列篩選器之下存取。 如果**Recordset**為階層式，目前的子系**資料錄集**和儲存及其子系，包括父代**資料錄集**。 如果**儲存**方法的子系**資料錄集**是呼叫，子系和所有子系都會儲存，但不是父代。 如需有關階層**資料錄集**，請參閱[資料成形](../../../ado/guide/data/data-shaping.md)。  
  
> [!NOTE]
>  儲存階層式時，適用某些限制**資料錄集**（資料圖形） 以 XML 格式。 如需詳細資訊，請參閱 <<c0> [ 保存的記錄，以 XML 格式](../../../ado/guide/data/persisting-records-in-xml-format.md)。
