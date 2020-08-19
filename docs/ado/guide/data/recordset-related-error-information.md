---
description: 資料錄集相關的錯誤資訊
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
ms.openlocfilehash: 7806d446c200f4d90ec458ceea268435ad9994e1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452950"
---
# <a name="recordset-related-error-information"></a>資料錄集相關的錯誤資訊
在批次處理期間，**記錄集**物件的**Status**屬性會提供**記錄集中**個別記錄的相關資訊。 在批次更新進行之前，**記錄集**的**Status**屬性會反映要加入、變更和刪除之記錄的相關資訊。 呼叫 **UpdateBatch** 之後， **Status** 屬性會指出作業成功或失敗。 當您在記錄 **集**內從記錄移至記錄時， **Status** 屬性的值會變更以描述目前記錄的狀態。
