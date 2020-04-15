---
title: 使用微軟元件服務 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], component services
- component services [ODBC]
ms.assetid: 06450562-d8f3-4987-b7bd-4a70223ff937
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fb5763058fa198cbad7464434e31942ef8d6cd7d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307579"
---
# <a name="using-microsoft-component-services"></a>使用 Microsoft Component Services
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 而是使用 Oracle 提供的 ODBC 驅動程式。  
  
 您可以使 Oracle 資料庫在 Microsoft Windows NT/Windows 2000 和 Microsoft Windows 95/98 上使用事務元件服務(如果正在使用 Windows NT)或 MTS。 為了使 Oracle 資料庫能夠與支援事務的元件服務一起工作,系統管理員應創建名為 V$XATRANS$的檢視。 要創建此文本,必須運行 Oracle 提供的文稿。 有關詳細資訊,請參閱元件服務説明或 Oracle 文件。
