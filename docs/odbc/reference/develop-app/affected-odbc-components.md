---
title: 受影響的 ODBC 元件 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- upgrading applications [ODBC], affected components
- application upgrades [ODBC], affected components
- compatibility [ODBC], affected components
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], affected components
ms.assetid: 71fa6ea4-007c-4c2b-b5af-2cec6ea79b58
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 22eb60ce88c0d7d0a623a90c202c77a9828e3a34
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793767"
---
# <a name="affected-odbc-components"></a>受影響的 ODBC 元件
回溯相容性，說明如何影響所引進的新版本的驅動程式管理員的應用程式、 驅動程式管理員，以及驅動程式。 這會影響應用程式和驅動程式時一個或兩個它們留在舊版本。 有，因此，三種類型的回溯相容性考量下, 表所示。  
  
|type|DM 版本|應用程式版本|驅動程式版本|  
|----------|-------------------|----------------------------|-----------------------|  
|為了與舊版相容的驅動程式管理員|*3.x*|*2.x*|*2.x*|  
|[1] 的驅動程式的回溯相容性|*3.x*|*2.x*|*3.x*|  
|應用程式的回溯相容性|*3.x*|*3.x*|*2.x*|  
  
 [附錄 g： 主要討論驅動程式 1] 的回溯相容性為了與舊版相容的驅動程式指導方針。  
  
> [!NOTE]
>  與標準相容的應用程式-例如，已寫入的 Open Group 或 ISO CLI 的標準為根據的應用程式保證適用於 ODBC *3.x*透過 ODBC 驅動程式*3.x*驅動程式管理員。 它會假設該應用程式使用的功能可用於驅動程式。 它也會假設使用 ODBC 的標準相容的應用程式，已編譯*3.x*標頭檔。
