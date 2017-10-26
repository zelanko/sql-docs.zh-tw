---
title: "使用 Microsoft Internet Information Services |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], IIS
- internet information services [ODBC]
- IIS [ODBC]
ms.assetid: 3328f2f1-b34a-472f-82cf-ad49768ff061
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 75659769b4d0318fa21494a3f2ca3262836c69eb
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="using-microsoft-internet-information-services"></a>使用 Microsoft Internet Information Services
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用由 Oracle 提供的 ODBC 驅動程式。  
  
 如果您無法從連接 IIS 指令碼 （特別是當您收到 ORA-TUT1-LESSON1-STEP2 12641 錯誤） 內，請將下列行加入 Sqlnet.ora 檔案：  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```  
  
 這會停用安全的網路服務，因此您可以使用匿名驗證來連接。

