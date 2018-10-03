---
title: 使用 Microsoft Internet Information Services |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], IIS
- internet information services [ODBC]
- IIS [ODBC]
ms.assetid: 3328f2f1-b34a-472f-82cf-ad49768ff061
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 509979a38e6d7e71f979ce317b9e1626a85c5a54
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47813936"
---
# <a name="using-microsoft-internet-information-services"></a>使用 Microsoft Internet Information Services
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用所提供的 ODBC 驅動程式。  
  
 如果您無法從連接中的 IIS 指令碼 （特別是當您收到 ORA 12641 錯誤），請將下面這一行加入 Sqlnet.ora 檔案：  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```  
  
 這會停用安全的網路服務，因此您可以使用匿名驗證來進行連接。
