---
title: "使用頁面 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- PageSize property [ADO]
- pages [ADO]
- Recordset object [ADO]
- AbsolutePage property [ADO]
- PageCount property [ADO]
ms.assetid: 442b08c5-ccc7-4192-a1cc-22f250867782
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 87c39965c7cf46c628aac17dd00fa3bf7ff18fdc
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="using-pages"></a>使用頁面
使用**PageCount**屬性來判斷多少頁的資料是在**資料錄集**物件。 *頁面*是群組的記錄，其大小等於**PageSize**屬性設定。 即使最後一頁不完整，因為有較少的記錄比**PageSize**值，它會計算為一個額外的頁面中**PageCount**值。 如果**資料錄集**物件不支援這個屬性， **PageCount**是-1 表示**PageCount**不確定。  
  
 使用**PageSize**屬性來判斷多少筆記錄組成一個邏輯頁面的資料。 建立頁面大小可讓您使用**AbsolutePage**移至特定頁面的第一個記錄的屬性。 當您想要讓使用者逐頁查看資料，一次檢視的記錄數目，這是 Web 伺服器案例中很有用。  
  
 這個屬性可以設定在任何時間，而且其值會用於計算特定的頁面上第一筆記錄的位置。  
  
 使用**AbsolutePage**屬性來識別目前的記錄所在的頁碼。 同樣地，提供者必須支援這個屬性才能使用適當的功能。  
  
 **AbsolutePage**是以 1 為基礎，並且等於 1，目前的記錄時的第一個記錄**資料錄集**。 設定這個屬性，以移至特定頁面的第一個記錄。 取得從總頁數**PageCount**屬性。
