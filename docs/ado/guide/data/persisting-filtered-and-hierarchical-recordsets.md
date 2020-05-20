---
title: 保存已篩選和階層式記錄集 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 5fa3fdd55fb78f16629907c174b08aab64ceb86e
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763109"
---
# <a name="persisting-filtered-and-hierarchical-recordsets"></a>保存篩選過的階層式資料錄集
如果[篩選器](../../../ado/reference/ado-api/filter-property.md)屬性對**記錄集**有效，只會儲存篩選器底下可存取的資料列。 如果**記錄集**是階層式，則會儲存目前的子**記錄集**和其子系，包括父**記錄集**。 如果呼叫子**記錄集**的**Save**方法，則會儲存子系及其所有子系，但父系則不會。 如需階層式**記錄集**的詳細資訊，請參閱[資料成形](../../../ado/guide/data/data-shaping.md)。  
  
> [!NOTE]
>  以 XML 格式儲存階層式**記錄集**（資料圖形）時，適用某些限制。 如需詳細資訊，請參閱[以 XML 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)。
