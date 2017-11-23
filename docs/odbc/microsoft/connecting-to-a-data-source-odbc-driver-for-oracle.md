---
title: "連接到資料來源 （如 Oracle 的 ODBC 驅動程式） |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connecting to data source [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connecting to data sources
ms.assetid: f724a9c5-342a-4f4e-a030-ec34f7378eaf
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b06651615b2e7578b277984c278d680ae9077f2c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="connecting-to-a-data-source-odbc-driver-for-oracle"></a>連接到資料來源 （如 Oracle 的 ODBC 驅動程式）
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用由 Oracle 提供的 ODBC 驅動程式。  
  
 ODBC 應用程式可以數種方式傳遞連接資訊。 例如，應用程式可能永遠會提示使用者輸入連接資訊的驅動程式。 或應用程式可能會預期有指定的資料來源連接的連接字串。 連接到資料來源的方式取決於您的 ODBC 應用程式所使用的連接方法。  
  
 若要連接到資料來源的一個常見方式是透過資料來源 對話方塊。 如果 ODBC 應用程式設定為使用對話方塊中，該對話方塊會顯示，而且會提示您輸入適當的資料來源連接資訊。  
  
 您也可以連接到資料來源使用[連接字串](../../odbc/microsoft/connection-string-format-and-attributes.md)。  
  
### <a name="to-connect-to-a-data-source-using-a-dialog-box"></a>若要連接到資料來源使用的對話方塊  
  
1.  資料來源 對話方塊出現時，請選取與 Oracle 資料來源，然後按一下 確定。 [連接] 對話方塊隨即出現。  
  
2.  填寫 [連接] 對話方塊中，針對適當的資訊，然後按一下 [確定]。  
  
 連線後會確認資訊，您的應用程式可以使用 oracle ODBC 驅動程式來存取資料來源包含的資訊。
