---
description: 使用頁面
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 71a4c9524090c85881e3aa194f7afbb3c11f0678
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452570"
---
# <a name="using-pages"></a>使用頁面
您可以使用 **PageCount** 屬性來判斷 **記錄集** 物件中有多少頁面的資料。 *頁面* 是其大小等於 **PageSize** 屬性設定的記錄群組。 即使最後一個頁面不完整，因為記錄比 **PageSize** 值少，因此它會計算為 **PageCount** 值中的額外頁面。 如果 **記錄集** 物件不支援這個屬性，則 **PageCount** 會是-1，表示 **PageCount** 為未知。  
  
 您可以使用 **PageSize** 屬性來判斷組成資料邏輯頁面的記錄數目。 建立頁面大小可讓您使用 **AbsolutePage** 屬性移至特定頁面的第一筆記錄。 當您想要允許使用者逐頁查看資料、一次查看特定的記錄數目時，這項功能就很有用。  
  
 您可以隨時設定這個屬性，其值將用來計算特定頁面之第一筆記錄的位置。  
  
 您可以使用 **AbsolutePage** 屬性來識別目前記錄所在的頁碼。 同樣地，提供者必須支援適當的功能，才能使用此屬性。  
  
 當目前記錄是**記錄集**內的第一筆記錄時， **AbsolutePage**是以1為基礎，而等於1。 將此屬性設定為移至特定頁面的第一筆記錄。 取得 **PageCount** 屬性中的總頁數。
