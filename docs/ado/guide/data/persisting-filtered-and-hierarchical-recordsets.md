---
title: 保存篩選與階層式資料錄集 |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- filtered Recordset persistence [ADO]
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: d01aeb4d-4e43-450b-b3f2-0c27eaaf9f86
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d945999ef7feb34ebe7de3b945868bc35c154589
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="persisting-filtered-and-hierarchical-recordsets"></a>保存篩選與階層式資料錄集
如果[篩選](../../../ado/reference/ado-api/filter-property.md)屬性實際上是針對**資料錄集**，儲存的資料列篩選器下存取。 如果**資料錄集**為階層式，目前的子系**資料錄集**和其子系會儲存包括父系**資料錄集**。 如果**儲存**方法的子系**資料錄集**是呼叫，都儲存在子系及其所有子系，但不是父代。 如需有關階層式**資料錄集**，請參閱[資料成形](../../../ado/guide/data/data-shaping.md)。  
  
> [!NOTE]
>  儲存階層式時，某些限制適用於**資料錄集**（資料圖形） 以 XML 格式。 如需詳細資訊，請參閱[XML 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)。
