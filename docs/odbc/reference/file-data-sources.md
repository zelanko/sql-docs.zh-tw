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
ms.openlocfilehash: 9d27f168640b25652ed0fd40154ebfb677ef9300
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68068640"
---
# <a name="file-data-sources"></a>檔案資料來源
檔案*資料來源*會儲存在檔案中，並允許單一使用者重複使用連接資訊，或在數個使用者之間共用。 使用檔案資料來源時，驅動程式管理員會使用 .dsn 檔案中的資訊來建立與資料來源的連接。 這個檔案可以像任何其他檔案一樣地操作。 檔案資料來源的資料來源名稱不是電腦資料來源，而且未註冊到任何一部使用者或電腦。  
  
 檔案資料來源會簡化連接程式，因為該 dsn 檔案包含的連接字串必須針對**SQLDriverConnect**函數的呼叫而建立。 Dsn 檔案的另一個優點是它可以複製到任何電腦，因此許多電腦都可以使用相同的資料來源，只要它們已安裝適當的驅動程式即可。 檔案資料來源也可以由應用程式共用。 可共用的檔案資料來源可以放在網路上，並由多個應用程式同時使用。  
  
 您也可以 unshareable 一個. dsn 檔案。 Unshareable 位於單一機器上，並指向機器資料來源。 Unshareable 檔資料來源主要是為了讓機器資料來源能夠輕鬆地轉換成檔案資料來源，讓應用程式可以設計成僅與檔案資料來源搭配使用。 當驅動程式管理員傳送 unshareable 檔資料來源中的資訊時，它會視需要連接到 .dsn 檔案所指向的機器資料來源。  
  
 如需有關檔案資料來源的詳細資訊，請參閱[使用檔案資料來源連接](../../odbc/reference/develop-app/connecting-using-file-data-sources.md)或[SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md)函數描述。
