---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 733b958ee883aa62034b4acc1eec67100b35a74d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47809266"
---
# <a name="file-data-sources"></a>檔案資料來源
*檔案資料來源*會儲存在檔案，並允許一位使用者重複使用或在數個使用者之間共用的連接資訊。 使用檔案資料來源時，驅動程式管理員會建立使用.dsn 檔案中的資訊的資料來源的連線。 就像任何其他檔案一樣，都可以操作這個檔案。 檔案資料來源沒有資料來源名稱，因為不機器資料來源，以及未註冊到任何一位使用者或電腦。  
  
 檔案資料來源可簡化連線程序，因為.dsn 檔案包含原本必須針對呼叫來建置連接字串**SQLDriverConnect**函式。 .Dsn 檔案的另一個優點是，可以將它複製到任何電腦，因此相同的資料來源可由多部機器，只要它們已安裝適當驅動程式。 應用程式也可以共用檔案資料來源。 可以放在網路上的共用資料來源，並同時使用多個應用程式。  
  
 .Dsn 檔案也可以是非共用。 留駐.dsn 檔案位於一部電腦上，並指向 機器資料來源。 自檔案資料來源存在主要是為了允許輕鬆轉換的機器資料來源為檔案資料來源，因此應用程式可以設計成僅使用檔案資料來源。 當驅動程式管理員會將資訊傳送自檔案資料來源中時，它會連線.dsn 檔案指向的機器資料來源所需。  
  
 如需檔案資料來源的詳細資訊，請參閱[連線使用的檔案資料來源](../../odbc/reference/develop-app/connecting-using-file-data-sources.md)，或有[SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md)函式描述。
