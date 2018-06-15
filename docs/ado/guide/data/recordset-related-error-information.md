---
title: 資料錄集相關的錯誤資訊 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset-related errors [ADO]
- errors [ADO], Recordset-related
ms.assetid: 7e103574-59ad-4790-b5f9-fa8d715e711e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 55f64646050eba8c76432c68c39b36b0daa9f4be
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35272347"
---
# <a name="recordset-related-error-information"></a>資料錄集相關的錯誤資訊
批次在處理期間，**狀態**屬性**資料錄集**物件提供資訊中的個別記錄**資料錄集**。 批次更新所需的位置，先**狀態**屬性**資料錄集**反映要加入、 變更和刪除記錄的相關資訊。 之後**UpdateBatch**呼叫之後**狀態**屬性會指出成功或失敗的作業。 當您移動記錄記錄**資料錄集**，值**狀態**屬性變更來描述目前記錄的狀態。
