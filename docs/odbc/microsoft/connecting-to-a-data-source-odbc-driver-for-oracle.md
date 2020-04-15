---
title: 連接到資料來源(Oracle 的 ODBC 驅動程式) |微軟文件
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
ms.openlocfilehash: 6ef567c9e3c7b63e7f5044de699750de856f3e52
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281298"
---
# <a name="connecting-to-a-data-source-odbc-driver-for-oracle"></a>連線到資料來源 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 而是使用 Oracle 提供的 ODBC 驅動程式。  
  
 ODBC 應用程式可以通過多種方式傳遞連接資訊。 例如,應用程式可能始終有驅動程式提示使用者提供連接資訊。 或者應用程式可能期望有一個指定數據源連接的連接字串。 連接到資料來源的方式取決於 ODBC 應用程式所使用的連接方法。  
  
 連接到數據源的一種常見方法是通過數據源對話方塊。 如果 ODBC 應用程式設定為使用對話框,將顯示該對話方塊並提示您輸入適當的資料來源連接資訊。  
  
 您還可以使用[連接字串](../../odbc/microsoft/connection-string-format-and-attributes.md)連接到資料來源。  
  
### <a name="to-connect-to-a-data-source-using-a-dialog-box"></a>使用對話框連接到資料來源  
  
1.  當出現「數據源」對話框時,選擇 Oracle 數據源,然後單擊「確定」。 將顯示"連接"對話框。  
  
2.  填寫"連接"對話框的相應資訊,然後單擊"確定"。  
  
 驗證連接資訊後,應用程式可以使用 Oracle 的 ODBC 驅動程式存取資料來源包含的資訊。
