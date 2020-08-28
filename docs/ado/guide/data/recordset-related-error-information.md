---
description: 資料錄集相關的錯誤資訊
title: 記錄集相關的錯誤資訊 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 454c62b969ee69e6186792ce77873c8c8fbb5704
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979809"
---
# <a name="recordset-related-error-information"></a>資料錄集相關的錯誤資訊
在批次處理期間，**記錄集**物件的**Status**屬性會提供**記錄集中**個別記錄的相關資訊。 在批次更新進行之前，**記錄集**的**Status**屬性會反映要加入、變更和刪除之記錄的相關資訊。 呼叫 **UpdateBatch** 之後， **Status** 屬性會指出作業成功或失敗。 當您在記錄 **集**內從記錄移至記錄時， **Status** 屬性的值會變更以描述目前記錄的狀態。
