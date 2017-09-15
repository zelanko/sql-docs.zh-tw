---
title: "驅動程式版本配置 |Microsoft 文件"
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
- ODBC driver for Oracle [ODBC], versions
ms.assetid: e4a8d9d7-8aba-48ab-8be6-1a6129adfb8f
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e3a8132d535b764818fb9dcab72b3cba8bb48154
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="driver-version-scheme"></a>驅動程式版本配置
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用由 Oracle 提供的 ODBC 驅動程式。  
  
 下表列出所有的 Microsoft ODBC Driver for Oracle 的發行的版本。  
  
|驅動程式版本|組建編號|可用性歷程|  
|--------------------|------------------|--------------------------|  
|1.0|2.00.6235|Visual c + + 4.2 和 Visual Basic 5.0 版，Enterprise Edition|  
|2.0|2.73.7269|Visual Studio 97 和 MDAC 1.5a|  
|2.0 更新|2.73.7283.01|IIS 4.0|  
|2.0 更新|2.73.7283.03|MDAC 1.5b 和 1.5 c|  
|2.0 更新|2.73.7356|ODBC 3.5 SDK|  
|2.5|2.573.2927|Visual Studio 6.0 和 MDAC 2.0|  
|2.5 更新|2.573.3513|SQL Server 7.0<br /><br /> SQL Server 6.5 SP5|  
  
 建置 2.00.6235 （第 1 版） 是 Microsoft ODBC Driver for Oracle 的第一個版本。 發行後的第一個版本，採用新的命名慣例。  
  
 例如，2.73.7283.03 可以分成下列主要元件：  
  
-   2 = 版本號碼。  
  
-   73 = 驅動程式專為其設計 Oracle 伺服器的版本。  
  
-   7283.03 = 驅動程式的組建編號。  
  
> [!NOTE]  
>  與發行版本 2.573.2973，導致一些混淆 2.573 是 2.73，比先前的版本，但每個區段的組建編號應該視為個別的命名慣例。 數字 573 大於 73，所以較新版本。 此外，「 2.5"表示驅動程式的版本號碼。
