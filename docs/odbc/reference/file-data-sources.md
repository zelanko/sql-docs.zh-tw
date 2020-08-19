---
description: 檔案資料來源
title: 檔案資料來源 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], file
- file data sources [ODBC]
ms.assetid: db245c80-981a-4638-bd03-69d04bc67af0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d02c767adab90ee4a7b6ff93a34886c03b87780c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429040"
---
# <a name="file-data-sources"></a>檔案資料來源
檔案*資料來源*會儲存在檔案中，並允許單一使用者重複使用連接資訊，或在數個使用者之間共用這些資訊。 使用檔案資料來源時，驅動程式管理員會使用一個 dsn 檔案中的資訊，建立與資料來源的連接。 這個檔案可以像任何其他檔案一樣操作。 檔案資料來源沒有資料來源名稱，如同電腦資料來源，而且未註冊至任何一個使用者或電腦。  
  
 檔案資料來源可簡化連接程式，因為 dsn 檔案包含的連接字串必須針對 **SQLDriverConnect** 函式的呼叫而建立。 該 dsn 檔的另一個優點是它可以複製到任何電腦，因此許多電腦都可以使用相同的資料來源，只要已安裝適當的驅動程式即可。 檔案資料來源也可以由應用程式共用。 可以在網路上放置可共用的檔案資料來源，並由多個應用程式同時使用。  
  
 也可以 unshareable dsn 檔案。 Unshareable 的 dsn 檔案位於單一電腦上，並指向電腦資料來源。 Unshareable 檔案資料來源的主要目的，是為了讓您輕鬆地將機器資料來源轉換成檔案資料來源，讓應用程式可以設計成僅搭配檔案資料來源使用。 當驅動程式管理員將資訊傳送至 unshareable 檔案資料來源時，它會視需要連接到 dsn 檔案所指向的電腦資料來源。  
  
 如需檔案資料來源的詳細資訊，請參閱 [使用檔案資料來源進行連接](../../odbc/reference/develop-app/connecting-using-file-data-sources.md)或 [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md) 函數描述。
