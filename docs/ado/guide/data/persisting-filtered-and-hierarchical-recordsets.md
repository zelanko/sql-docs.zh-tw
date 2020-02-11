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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 11ab68775e19ec1d3ce3c888917588f41ad65287
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924633"
---
# <a name="persisting-filtered-and-hierarchical-recordsets"></a>保存篩選過的階層式資料錄集
如果[篩選器](../../../ado/reference/ado-api/filter-property.md)屬性對**記錄集**有效，只會儲存篩選器底下可存取的資料列。 如果**記錄集**是階層式，則會儲存目前的子**記錄集**和其子系，包括父**記錄集**。 如果呼叫子**記錄集**的**Save**方法，則會儲存子系及其所有子系，但父系則不會。 如需階層式**記錄集**的詳細資訊，請參閱[資料成形](../../../ado/guide/data/data-shaping.md)。  
  
> [!NOTE]
>  以 XML 格式儲存階層式**記錄集**（資料圖形）時，適用某些限制。 如需詳細資訊，請參閱[以 XML 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)。
