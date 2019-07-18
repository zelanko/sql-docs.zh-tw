---
title: 資料錄集相關的錯誤資訊 |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924379"
---
# <a name="recordset-related-error-information"></a>資料錄集相關的錯誤資訊
批次在處理期間，**狀態**屬性**Recordset**物件提供在個別的記錄資訊**資料錄集**。 批次更新所需的位置，再**狀態**屬性**資料錄集**反映要加入、 變更和刪除的記錄資訊。 在後**UpdateBatch**已呼叫**狀態**屬性會指出成功或失敗的作業。 當您移動記錄間**Recordset**的值**狀態**屬性變更，來描述目前記錄的狀態。
