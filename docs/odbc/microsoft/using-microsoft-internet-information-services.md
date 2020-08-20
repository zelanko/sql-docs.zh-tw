---
description: 使用 Microsoft Internet Information Services
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5e20a15aad4409f535d83e813fdfbd911ca80674
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471330"
---
# <a name="using-microsoft-internet-information-services"></a>使用 Microsoft Internet Information Services
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 提供的 ODBC 驅動程式。  
  
 如果您無法從 IIS 腳本內連接 (特別是當您收到 TNSNAMES.ORA-12641 錯誤) 時，請將下列這一行新增至 Sqlnet.ora tnsnames.ora 檔案：  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```  
  
 這將會停用安全的網路服務，讓您可以使用匿名驗證來連接。
