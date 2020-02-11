---
title: 使用 Microsoft 元件服務 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 91d6dcf0ca7f87d6ed510d582f7a7ba0f80e8c74
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088154"
---
# <a name="using-microsoft-component-services"></a>使用 Microsoft Component Services
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 所提供的 ODBC 驅動程式。  
  
 您可以讓 Oracle 資料庫在 Microsoft Windows NT/Windows 2000 和 Microsoft Windows 95/98 上使用交易式元件服務（如果您使用的是 Windows NT，則是 MTS）。 若要讓 Oracle 資料庫使用支援交易的元件服務，系統管理員應該建立名為 V $ XATRANS $ 的視圖。 若要建立此腳本，您必須執行 Oracle 提供的腳本。 如需詳細資訊，請參閱元件服務協助或 Oracle 檔。
