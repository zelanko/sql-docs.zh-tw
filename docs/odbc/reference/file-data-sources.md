---
title: 檔案資料來源 :微軟文件
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
ms.openlocfilehash: 0661aa424a7a118b8b12f4bf8433987ff83bd788
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306649"
---
# <a name="file-data-sources"></a>檔案資料來源
*檔案數據來源*儲存在檔案中,並允許單個使用者重複使用連接資訊或在多個用戶之間共用。 使用檔案資料來源時,驅動程式管理器使用 .dsn 檔案中的資訊與數據源建立連接。 此檔可以像任何其他檔一樣作。 檔資料來源沒有資料來源名稱,電腦數據來源也是如此,並且不註冊給任何一個使用者或電腦。  
  
 檔案資料來源簡化了連接過程,因為 .dsn 檔包含連接字串,否則必須為呼叫**SQLDriverConnect**函數生成連接字串。 .dsn 檔的另一個優點是它可以複製到任何計算機,因此只要安裝了適當的驅動程式,許多計算機就可以使用相同的數據源。 應用程式也可以共用文件數據來源。 可共用的文件數據源可以放置在網路上,並由多個應用程式同時使用。  
  
 .dsn 檔也可以不可共用。 不可共用的 .dsn 檔案駐留在一台電腦上,並指向計算機數據源。 存在不可共用的文件數據來源主要是為了允許將計算機數據源輕鬆轉換為檔數據來源,以便應用程式可以設計為僅處理檔資料來源。 當驅動程式管理員在不可共用的檔案數據來源中發送資訊時,它將根據需要連接到 .dsn 檔指向的計算機數據來源。  
  
 有關文件資料來源的詳細資訊,請參閱[使用檔案資料源進行連接](../../odbc/reference/develop-app/connecting-using-file-data-sources.md)或[SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md)函數描述。
