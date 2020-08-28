---
description: 保存篩選過的階層式資料錄集
title: 保存篩選和階層式記錄集 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: fc18622d3fda977d4a19d9946430c9e1cd0b2444
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980089"
---
# <a name="persisting-filtered-and-hierarchical-recordsets"></a>保存篩選過的階層式資料錄集
如果 [篩選](../../../ado/reference/ado-api/filter-property.md) 屬性適用于 **記錄集**，則只會儲存篩選下的可存取資料列。 如果 **記錄集** 是階層式的，則會儲存目前的子 **記錄集** 和其子系，包括父 **記錄集**。 如果呼叫子**記錄集**的**Save**方法，則會儲存子系及其所有子系，但父系則否。 如需階層式 **記錄集**的詳細資訊，請參閱 [資料成形](../../../ado/guide/data/data-shaping.md)。  
  
> [!NOTE]
>  將階層式 **記錄集** 儲存 (資料圖形) 為 XML 格式時，會有一些限制。 如需詳細資訊，請參閱 [以 XML 格式保存記錄](../../../ado/guide/data/persisting-records-in-xml-format.md)。
