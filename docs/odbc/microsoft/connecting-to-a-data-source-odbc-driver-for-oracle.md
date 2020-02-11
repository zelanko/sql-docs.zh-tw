---
title: 連接到資料來源（ODBC Driver for Oracle） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b0e9e62c8e03166ec2f76b1c6bcb5000a062bac3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68082043"
---
# <a name="connecting-to-a-data-source-odbc-driver-for-oracle"></a>連線到資料來源 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 所提供的 ODBC 驅動程式。  
  
 ODBC 應用程式可以透過數種方式傳遞連接資訊。 例如，應用程式可能會讓驅動程式一律提示使用者輸入連接資訊。 或者，應用程式可能會預期會指定資料來源連接的連接字串。 連接到資料來源的方式，取決於 ODBC 應用程式所使用的連接方法。  
  
 連接到資料來源的其中一個常見方式是透過 [資料來源] 對話方塊。 如果您的 ODBC 應用程式已設定為使用對話方塊，則會顯示該對話方塊，並提示您輸入適當的資料來源連接資訊。  
  
 您也可以使用[連接字串](../../odbc/microsoft/connection-string-format-and-attributes.md)來連接到資料來源。  
  
### <a name="to-connect-to-a-data-source-using-a-dialog-box"></a>若要使用對話方塊來連接到資料來源  
  
1.  [資料來源] 對話方塊出現時，請選取 Oracle 資料來源，然後按一下 [確定]。 [連接] 對話方塊隨即出現。  
  
2.  填入 [連接] 對話方塊的適當資訊，然後按一下 [確定]。  
  
 驗證連接資訊之後，您的應用程式就可以使用 ODBC Driver for Oracle 來存取資料來源所包含的資訊。
