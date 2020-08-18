---
description: 驅動程式版本配置
title: 驅動程式版本配置 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], versions
ms.assetid: e4a8d9d7-8aba-48ab-8be6-1a6129adfb8f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0414da00ffc5a220e3bf6b13837880b1116f58eb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412724"
---
# <a name="driver-version-scheme"></a>驅動程式版本配置
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 提供的 ODBC 驅動程式。  
  
 下表列出 Microsoft ODBC Driver for Oracle 的所有發行版本。  
  
|驅動程式版本|組建編號|可用性歷程|  
|--------------------|------------------|--------------------------|  
|1.0|2.00.6235|Visual C++ 4.2 和 Visual Basic 5.0，Enterprise Edition|  
|2.0|2.73.7269|Visual Studio 97 和 MDAC 1.5 a|  
|2.0 已更新|2.73.7283.01|IIS 4。0|  
|2.0 已更新|2.73.7283.03|MDAC 1.5 b 和 1.5 c|  
|2.0 已更新|2.73.7356|ODBC 3.5 SDK|  
|2.5|2.573.2927|Visual Studio 6.0 和 MDAC 2。0|  
|2.5 已更新|2.573.3513|SQL Server 7。0<br /><br /> SQL Server 6.5 SP5|  
  
 Build 2.00.6235 (第1版) 是 Microsoft ODBC Driver for Oracle 的第一版。 第一個版本發行之後，採用新的命名慣例。  
  
 例如，2.73.7283.03 可以分成下列相異元件：  
  
-   2 = 版本號碼。  
  
-   73 = 驅動程式所設計的 Oracle 伺服器版本。  
  
-   7283.03 = 驅動程式的組建編號。  
  
> [!NOTE]  
>  使用 release 2.573.2973 時，命名慣例會導致一些混淆，即2.573 是比2.73 更早的版本，但組建編號的每個區段都應個別考慮。 數位573大於73，因此是較新的版本。 此外，"2.5" 表示驅動程式的版本號碼。
