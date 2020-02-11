---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d8a155f5d76e8a250c64d3d59e160fbb5863414f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68071850"
---
# <a name="driver-version-scheme"></a>驅動程式版本配置
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 所提供的 ODBC 驅動程式。  
  
 下表列出 Microsoft ODBC Driver for Oracle 的所有發行版本。  
  
|驅動程式版本|組建編號|可用性歷程記錄|  
|--------------------|------------------|--------------------------|  
|1.0|2.00.6235|Visual C++ 4.2 和 Visual Basic 5.0，Enterprise Edition|  
|2.0|2.73.7269|Visual Studio 97 和 MDAC 1.5 a|  
|2.0 已更新|2.73.7283.01|IIS 4。0|  
|2.0 已更新|2.73.7283.03|MDAC 1.5 b 和 1.5 c|  
|2.0 已更新|2.73.7356|ODBC 3.5 SDK|  
|2.5|2.573.2927|Visual Studio 6.0 和 MDAC 2。0|  
|2.5 已更新|2.573.3513|SQL Server 7。0<br /><br /> SQL Server 6.5 SP5|  
  
 Build 2.00.6235 （版本1）是 Microsoft ODBC Driver for Oracle 的第一版。 第一版發行之後，採用了新的命名慣例。  
  
 例如，2.73.7283.03 可以分成下列不同的元件：  
  
-   2 = 版本號碼。  
  
-   73 = 驅動程式設計所在的 Oracle 伺服器版本。  
  
-   7283.03 = 驅動程式的組建編號。  
  
> [!NOTE]  
>  使用 release 2.573.2973 時，命名慣例會造成一些混淆，即2.573 是比2.73 更早的版本，但組建編號的每個區段都應該個別考慮。 數位573大於73，因此是較新的版本。 此外，"2.5" 表示驅動程式的版本號碼。
