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
manager: craigg
ms.openlocfilehash: c4f13a77a9f03aa76fccc41a1fa19878dd935db0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47636806"
---
# <a name="recordset-related-error-information"></a>資料錄集相關的錯誤資訊
批次在處理期間，**狀態**屬性**Recordset**物件提供在個別的記錄資訊**資料錄集**。 批次更新所需的位置，再**狀態**屬性**資料錄集**反映要加入、 變更和刪除的記錄資訊。 在後**UpdateBatch**已呼叫**狀態**屬性會指出成功或失敗的作業。 當您移動記錄間**Recordset**的值**狀態**屬性變更，來描述目前記錄的狀態。
