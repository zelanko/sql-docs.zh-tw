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
author: rothja
ms.author: jroth
ms.openlocfilehash: cb51fa80cff0a17340e289886f0315ea167b88b0
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760954"
---
# <a name="recordset-related-error-information"></a>資料錄集相關的錯誤資訊
在批次處理期間，**記錄集**物件的**Status**屬性會提供有關**記錄集中**個別記錄的資訊。 進行批次更新之前，**記錄集**的**Status**屬性會反映要新增、變更及刪除之記錄的相關資訊。 呼叫**UpdateBatch**之後， **Status**屬性會指出作業成功或失敗。 當您從記錄檔移至記錄**集**內的記錄時， **Status**屬性的值會變更以描述目前記錄的狀態。
