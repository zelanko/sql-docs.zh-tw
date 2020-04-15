---
title: 驅動程式版本方案 |微軟文件
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
ms.openlocfilehash: 864a8bd892315b060fc6fcf42dbe69dfea61ae59
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303449"
---
# <a name="driver-version-scheme"></a>驅動程式版本配置
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 而是使用 Oracle 提供的 ODBC 驅動程式。  
  
 下表列出了 Oracle 的 Microsoft ODBC 驅動程式的所有已發表版本。  
  
|驅動程式版本|組建編號|可用性歷程|  
|--------------------|------------------|--------------------------|  
|1.0|2.00.6235|視覺C++ 4.2 和視覺基礎 5.0,企業版|  
|2.0|2.73.7269|視覺工作室 97 和 MDAC 1.5a|  
|2.0 已更新|2.73.7283.01|IIS 4.0|  
|2.0 已更新|2.73.7283.03|MDAC 1.5b 和 1.5c|  
|2.0 已更新|2.73.7356|ODBC 3.5 SDK|  
|2.5|2.573.2927|視覺工作室 6.0 和 MDAC 2.0|  
|2.5 更新|2.573.3513|SQL 伺服器 7.0<br /><br /> SQL 伺服器 6.5 SP5|  
  
 版本 2.00.6235(版本 1)是 Oracle 的 Microsoft ODBC 驅動程式的第一個版本。 在第一個版本發佈后,通過了新的命名約定。  
  
 例如,2.73.7283.03 可以分為以下不同的元件:  
  
-   2 = 版本號。  
  
-   73 = 為其設計驅動程式的 Oracle 伺服器版本。  
  
-   7283.03 = 驅動程式的生成編號。  
  
> [!NOTE]  
>  對於版本 2.573.2973,命名約定導致一些混淆,即 2.573 是比 2.73 更早版本,但生成編號的每個部分都應單獨考慮。 數位 573 大於 73,因此它是一個較新版本。 此外,「2.5」表示驅動程式的版本號。
