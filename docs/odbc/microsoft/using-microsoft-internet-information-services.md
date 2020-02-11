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
ms.openlocfilehash: 9e531149af21facd80e9e6ddab19a76c3bdc0fa6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088139"
---
# <a name="using-microsoft-internet-information-services"></a>使用 Microsoft Internet Information Services
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 所提供的 ODBC 驅動程式。  
  
 如果您無法從 IIS 腳本內連接（特別是當您收到 TNSNAMES.ORA-12641 錯誤時），請將下行新增至 Sqlnet.ora. tnsnames.ora 檔案：  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```  
  
 這會停用安全網絡服務，讓您可以使用匿名驗證進行連接。
