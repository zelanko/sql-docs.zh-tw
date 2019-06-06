---
title: 使用頁面 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- PageSize property [ADO]
- pages [ADO]
- Recordset object [ADO]
- AbsolutePage property [ADO]
- PageCount property [ADO]
ms.assetid: 442b08c5-ccc7-4192-a1cc-22f250867782
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6afd68ddf99799288939eeb0c6522275ec4d273f
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704535"
---
# <a name="using-pages"></a>使用頁面
使用**PageCount**屬性來判斷多少頁的資料是在**資料錄集**物件。 *頁面*是一組的記錄，其大小等於**PageSize**屬性設定。 即使最後一頁是不完整，因為有較少的記錄，比**PageSize**的值，它會計算為中的其他頁面**PageCount**值。 如果**Recordset**物件不支援這個屬性， **PageCount**會是-1 表示**PageCount**不確定。  
  
 使用**PageSize**屬性來判斷多少筆記錄組成一個邏輯頁面的資料。 建立以頁面大小可讓您使用**AbsolutePage**移至特定的頁面上第一筆記錄的屬性。 當您想要讓使用者逐頁查看資料，一次檢視的記錄數目，這是在 Web 伺服器案例中有用的。  
  
 這個屬性可以設定在任何時間，和其值會用於計算特定網頁的第一筆記錄的位置。  
  
 使用**AbsolutePage**屬性來識別目前的記錄所在的頁面數目。 同樣地，提供者必須支援這個屬性才能使用適當的功能。  
  
 **AbsolutePage**是以 1 為基礎，並等於 1，當目前的記錄中的第一個記錄**資料錄集**。 設定這個屬性，以移至特定的頁面上第一筆記錄。 取得從總頁數**PageCount**屬性。
