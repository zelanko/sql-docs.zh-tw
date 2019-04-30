---
title: 編輯現有的記錄 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], existing records
ms.assetid: 17ce1263-5897-452a-9ea5-c7f96b33df65
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 64262ae52b802398fc2060092a03e7469146f063
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63161725"
---
# <a name="editing-existing-records"></a>編輯現有的記錄
若要編輯現有的記錄，請移至您想要編輯和變更的資料列**值**您想要變更的欄位的屬性。 如需詳細資訊**欄位**物件的**值**屬性，請參閱[檢查資料](../../../ado/guide/data/examining-data.md)。 根據您的資料指標類型，您將使用**更新**或是**UpdateBatch**將變更傳送回資料來源。 如需詳細資訊，請參閱 <<c0> [ 更新和保存資料](../../../ado/guide/data/updating-and-persisting-data.md)。  
  
 它會使用預存程序與命令物件執行更新，以及對於執行其他作業，因為預存程序不需要建立資料指標通常更有效率。 如需有關資料指標的詳細資訊，請參閱 <<c0> [ 了解資料指標和鎖定](../../../ado/guide/data/understanding-cursors-and-locks.md)。
