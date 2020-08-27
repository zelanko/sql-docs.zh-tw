---
description: 編輯現有的記錄
title: 編輯現有的記錄 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], existing records
ms.assetid: 17ce1263-5897-452a-9ea5-c7f96b33df65
author: rothja
ms.author: jroth
ms.openlocfilehash: 35c2376031e96a19c4a761a9826e47be2306518e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991329"
---
# <a name="editing-existing-records"></a>編輯現有的記錄
若要編輯現有的記錄，請移至您想要編輯的資料列，然後變更您要變更之欄位的 [ **值** ] 屬性。 如需 **Field** 物件的 **Value** 屬性的詳細資訊，請參閱 [檢查資料](./examining-data.md)。 視您的資料指標類型而定，您將使用 **Update** 或 **UpdateBatch** 將變更傳送回資料來源。 如需詳細資訊，請參閱 [更新和保存資料](./updating-and-persisting-data.md)。  
  
 通常更有效率的方式是使用預存程式搭配 command 物件來執行更新，以及執行其他作業，因為預存程式不需要建立資料指標。 如需資料指標的詳細資訊，請參閱 [瞭解資料指標和鎖定](./understanding-cursors-and-locks.md)。