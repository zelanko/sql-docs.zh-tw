---
title: 檔案資料來源 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], file
- file data sources [ODBC]
ms.assetid: db245c80-981a-4638-bd03-69d04bc67af0
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 25be6ea116b5449de55aeb8a16ed1cf12e1ce418
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32915583"
---
# <a name="file-data-sources"></a>檔案資料來源
*檔案資料來源*儲存在檔案，並允許重複使用由單一使用者或數個使用者之間共用的連接資訊。 使用檔案資料來源時，驅動程式管理員會建立使用.dsn 檔案中的資訊的資料來源的連線。 這個檔案，即可像任何其他檔案一樣操作。 檔案資料來源沒有資料來源名稱，不會機器資料來源，以及未登錄至任何一個使用者或電腦。  
  
 檔案資料來源來簡化連線程序，因為.dsn 檔案包含原本必須針對呼叫的連接字串**SQLDriverConnect**函式。 .Dsn 檔案的另一個好處是，可以將它複製到任何電腦上，因此相同的資料來源可供許多機器只要有適當的驅動程式安裝。 應用程式也可以共用檔案資料來源。 可共用的檔案資料來源可以放在網路上，並同時使用多個應用程式。  
  
 也可以是非共用.dsn 檔案。 自.dsn 檔案位於單一電腦上，並指向 機器資料來源。 自檔案資料來源存在目的主要是為了允許輕鬆轉換機器資料來源為檔案資料來源，讓應用程式可以設計為只使用檔案資料來源。 當驅動程式管理員會將資訊傳送自檔案資料來源中時，連接視.dsn 檔案會指向機器資料來源。  
  
 如需檔案資料來源的詳細資訊，請參閱[連接使用的檔案資料來源](../../odbc/reference/develop-app/connecting-using-file-data-sources.md)，或[SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md)函式描述。
