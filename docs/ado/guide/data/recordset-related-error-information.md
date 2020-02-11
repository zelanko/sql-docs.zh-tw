---
title: 記錄集相關的錯誤資訊 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset-related errors [ADO]
- errors [ADO], Recordset-related
ms.assetid: 7e103574-59ad-4790-b5f9-fa8d715e711e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d3f8e8d9802b5d0c73af73aff20d929c188b9292
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924379"
---
# <a name="recordset-related-error-information"></a>資料錄集相關的錯誤資訊
在批次處理期間，**記錄集**物件的**Status**屬性會提供有關**記錄集中**個別記錄的資訊。 進行批次更新之前，**記錄集**的**Status**屬性會反映要新增、變更及刪除之記錄的相關資訊。 呼叫**UpdateBatch**之後， **Status**屬性會指出作業成功或失敗。 當您從記錄檔移至記錄**集**內的記錄時， **Status**屬性的值會變更以描述目前記錄的狀態。
