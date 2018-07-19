---
title: 使用 Microsoft 元件服務 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], component services
- component services [ODBC]
ms.assetid: 06450562-d8f3-4987-b7bd-4a70223ff937
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a297d64708383edf997cbb6adf3b7d72aed53969
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32914423"
---
# <a name="using-microsoft-component-services"></a>使用 Microsoft 元件服務
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用由 Oracle 提供的 ODBC 驅動程式。  
  
 您可以在 Microsoft Windows NT/Windows 2000 和 Microsoft Windows 95/98 上啟用的 Oracle 資料庫，才能使用交易式元件服務 （或 MTS，如果您使用 Windows NT）。 若要啟用 Oracle 資料庫來使用元件服務支援交易，系統管理員應該建立名為 V$ XATRANS$ 檢視。 若要建立此指令碼，您必須執行 Oracle 提供的指令碼。 如需詳細資訊，請參閱元件服務說明或 Oracle 文件。
