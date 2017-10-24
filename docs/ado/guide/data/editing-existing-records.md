---
title: "編輯現有記錄 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- editing data [ADO], existing records
ms.assetid: 17ce1263-5897-452a-9ea5-c7f96b33df65
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 03e720476c8056737e2735ac96c97a7caf190de4
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="editing-existing-records"></a>編輯現有的資料錄
若要編輯現有的記錄，請移至您想要編輯並變更的資料列**值**您想要變更的欄位的屬性。 如需有關**欄位**物件的**值**屬性，請參閱[檢查資料](../../../ado/guide/data/examining-data.md)。 根據您的資料指標類型，您將使用**更新**或**UpdateBatch**將變更傳送回資料來源。 如需詳細資訊，請參閱[正在更新及保存資料](../../../ado/guide/data/updating-and-persisting-data.md)。  
  
 它會使用預存程序與命令物件執行更新，以及對於執行其他作業，因為預存程序不需要建立資料指標通常更有效率。 如需資料指標的詳細資訊，請參閱[了解資料指標和鎖定](../../../ado/guide/data/understanding-cursors-and-locks.md)。

