---
description: 設定 ODBC Driver for Oracle
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f53bf5efc66ad260c0184baf95a254313319da5d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483671"
---
# <a name="configuring-the-odbc-driver-for-oracle"></a>設定 ODBC Driver for Oracle
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 提供的 ODBC 驅動程式。  
  
 您可以藉由瞭解資料環境，並透過 [ [ODBC 資料來源管理員](../../odbc/admin/odbc-data-source-administrator.md) ] 對話方塊或透過連接字串參數，正確設定資料來源連接的參數，來控制 ODBC Driver for Oracle 的效能。 對話方塊會提供下列控制項，以使用對話方塊或使用連接字串連接到資料來源：  
  
-   [**使用者 DSN]** 索引標籤列出電腦本機的資料來源名稱。  
  
-   [**系統 DSN]** 索引標籤可讓您新增或移除系統資料來源。 本機電腦上的所有使用者都可以存取系統資料來源。  
  
-   [檔案**DSN]** 索引標籤可讓您新增或移除本機電腦上的檔案資料來源。 已安裝相同驅動程式的所有使用者都可以共用檔案資料來源。  
  
-   **驅動程式** 索引標籤列出已安裝的 ODBC 驅動程式。  
  
-   [**追蹤]** 索引標籤可讓您指定 ODBC 驅動程式管理員如何追蹤對 ODBC 函數的呼叫。 您可以針對每個已安裝的 ODBC 應用程式分別設定追蹤。  
  
-   [**連接共用]** 索引標籤可讓您為每個已安裝的驅動程式選取連接選項。  
  
-   **關於** 索引標籤列出已安裝的 ODBC 元件檔案。  
  
 加入資料來源之後，您可以使用 [ **ODBC 資料來源管理員** ] 對話方塊來設定資料來源的存取權。 選取資料來源，然後按一下其中一個索引標籤，以編輯或審核資訊。
