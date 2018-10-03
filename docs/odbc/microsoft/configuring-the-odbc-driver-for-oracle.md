---
title: 設定 ODBC Driver for Oracle |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- configuring ODBC driver for Oracle [ODBC]
- ODBC driver for Oracle [ODBC], configuring
ms.assetid: 0a5f827c-0b80-4627-85cb-f10292b9fb33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ae444cfb293e12bd94281957335da1d4f4a97885
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47831452"
---
# <a name="configuring-the-odbc-driver-for-oracle"></a>設定 ODBC Driver for Oracle
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用所提供的 ODBC 驅動程式。  
  
 您可以藉由了解資料環境，並正確設定之參數的資料來源連接，透過控制適用於 Oracle 的 ODBC 驅動程式的效能[ODBC 資料來源管理員](../../odbc/admin/odbc-data-source-administrator.md)對話方塊方塊中，或用來連線字串參數。 對話方塊中提供下列控制項連接到使用對話方塊中的資料來源，或使用連接字串：  
  
-   **使用者 DSN 索引標籤**列出本機電腦的資料來源名稱。  
  
-   **系統 DSN 索引標籤**可讓您新增或移除系統資料來源。 可以在本機電腦上的所有使用者存取系統資料來源。  
  
-   **檔案 DSN 索引標籤**可讓您新增或移除本機電腦上的檔案資料來源。 可由具有相同的驅動程式安裝的所有使用者共用檔案資料來源。  
  
-   **驅動程式 索引標籤**會列出已安裝的 ODBC 驅動程式。  
  
-   **追蹤索引標籤**可讓您指定 ODBC 驅動程式管理員如何追蹤呼叫 ODBC 函數。 您可以設定個別追蹤每個已安裝的 ODBC 應用程式。  
  
-   **連線共用 索引標籤**可讓您選取每個已安裝的驅動程式的連線選項。  
  
-   **索引標籤的相關**列出已安裝的 ODBC 元件檔案。  
  
 新增資料來源之後，您可以使用**ODBC 資料來源管理員**對話方塊來設定您的資料來源的存取。 選取資料來源，然後按一下其中一個索引標籤來編輯或檢視的資訊。
