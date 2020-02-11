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
ms.openlocfilehash: ce8679c0c7b20dfaa641918f0447a2f77bfd474a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67925447"
---
# <a name="editing-existing-records"></a>編輯現有的記錄
若要編輯現有的記錄，請移至您想要編輯的資料列，並變更您想要變更之欄位的**Value**屬性。 如需**欄位**物件之**Value**屬性的詳細資訊，請參閱[檢查資料](../../../ado/guide/data/examining-data.md)。 視您的資料指標類型而定，您將使用**Update**或**UpdateBatch**將變更傳送回資料來源。 如需詳細資訊，請參閱[更新和保存資料](../../../ado/guide/data/updating-and-persisting-data.md)。  
  
 使用預存程式搭配命令物件來執行更新，以及執行其他作業，通常會更有效率，因為預存程式不需要建立資料指標。 如需資料指標的詳細資訊，請參閱[瞭解資料指標和鎖定](../../../ado/guide/data/understanding-cursors-and-locks.md)。
