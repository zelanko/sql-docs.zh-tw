---
title: 使用 SQLDriverConnect 連接 |Microsoft Docs
description: SQLDriverConnect 透過 SQLConnect 提供額外的連接功能，包括提示使用者提供詳細資訊的選項。
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- functions [ODBC], data source or driver connections
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- SQLDriverConnect function [ODBC], connecting
- connection functions [ODBC]
- ODBC drivers [ODBC], connection functions
ms.assetid: e46e959f-d3c5-4ddb-810a-107bfcb83fd2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 78186e903405aa1b59cfac185e62646dbda6e77a
ms.sourcegitcommit: dc8a30a4a27e15fc6671ca2674da9b7c637ec255
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/21/2020
ms.locfileid: "88746168"
---
# <a name="connecting-with-sqldriverconnect"></a>使用 SQLDriverConnect 進行連線

**SQLDriverConnect** 是用來連接到使用連接字串的資料來源。 在下列案例中，會使用**SQLDriverConnect** ，而不是**SQLConnect** ：  
  
- 使用包含資料來源名稱、一或多個使用者識別碼、一或多個密碼，以及資料來源所需的其他資訊的連接字串來建立連接。  
  
- 使用部分連接字串或沒有其他資訊來建立連接;在此情況下，驅動程式管理員和驅動程式都會提示使用者提供連接資訊。  
  
- 建立未在系統資訊中定義之資料來源的連接。 如果應用程式提供部分連接字串，驅動程式可能會提示使用者輸入連接資訊。  
  
- 使用從 dsn 檔案中的資訊所建立的連接字串，建立與資料來源的連接。  
  
建立連接之後， **SQLDriverConnect** 會傳回已完成的連接字串。 應用程式可以將此字串用於後續的連接要求。

此章節包含下列主題。  
  
- [特定驅動程式的連線資訊](driver-specific-connection-information.md)  
  
- [提示使用者輸入連線資訊](prompting-the-user-for-connection-information.md)  
  
- [使用檔案資料來源進行連線](connecting-using-file-data-sources.md)  
  
- [直接連線到驅動程式](connecting-directly-to-drivers.md)
