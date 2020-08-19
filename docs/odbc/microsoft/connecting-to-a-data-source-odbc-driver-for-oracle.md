---
description: 連線到資料來源 (ODBC Driver for Oracle)
title: 連接到資料來源 (ODBC Driver for Oracle) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to data source [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connecting to data sources
ms.assetid: f724a9c5-342a-4f4e-a030-ec34f7378eaf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6951dd89f3ad1a311d93aca460c61dc7317b2f30
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483661"
---
# <a name="connecting-to-a-data-source-odbc-driver-for-oracle"></a>連線到資料來源 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 提供的 ODBC 驅動程式。  
  
 ODBC 應用程式可以透過數種方式傳遞連接資訊。 例如，應用程式可能會讓驅動程式永遠提示使用者輸入連接資訊。 或者，應用程式可能預期會有指定資料來源連接的連接字串。 連接至資料來源的方式取決於 ODBC 應用程式所使用的連接方法。  
  
 連接到資料來源的其中一個常見方式是透過 [資料來源] 對話方塊。 如果您的 ODBC 應用程式設定為使用對話方塊，則會顯示該對話方塊，並提示您輸入適當的資料來源連接資訊。  
  
 您也可以使用 [連接字串](../../odbc/microsoft/connection-string-format-and-attributes.md)連接到資料來源。  
  
### <a name="to-connect-to-a-data-source-using-a-dialog-box"></a>使用對話方塊連接到資料來源  
  
1.  當 [資料來源] 對話方塊出現時，選取 Oracle 資料來源，然後按一下 [確定]。 [連接] 對話方塊隨即出現。  
  
2.  在 [連接] 對話方塊中填入適當的資訊，然後按一下 [確定]。  
  
 驗證連接資訊之後，您的應用程式可以使用 ODBC Driver for Oracle 來存取資料來源所包含的資訊。
