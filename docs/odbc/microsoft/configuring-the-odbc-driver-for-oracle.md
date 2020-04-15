---
title: 設定 Oracle 的 ODBC 驅動程式 |微軟文件
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
ms.openlocfilehash: 1bbdbe36ed9e6f254e2b738479698bd9eece09f8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281368"
---
# <a name="configuring-the-odbc-driver-for-oracle"></a>設定 ODBC Driver for Oracle
> [!IMPORTANT]  
>  此功能將在將來版本的 Windows 中刪除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 而是使用 Oracle 提供的 ODBC 驅動程式。  
  
 您可以通過瞭解資料環境並透過[ODBC 資料來源管理員](../../odbc/admin/odbc-data-source-administrator.md)對話方塊或透過連接字串參數正確設定資料來源連接的參數來控制 Oracle 的 ODBC 驅動程式的效能。 這個對話框提供以下控制項,用於使用對話框或使用連接字串連接到資料來源:  
  
-   **使用者 DSN 選項卡**列出電腦本地的資料來源名稱。  
  
-   **系統 DSN 選項卡**讓您能夠新增或刪除系統資料來源。 本地電腦上的所有使用者都可以訪問系統數據來源。  
  
-   **檔案 DSN 選項卡**讓您可以從本地電腦加入或刪除檔案資料來源。 檔數據源可以由安裝了相同驅動程式的所有用戶共用。  
  
-   **驅動程式選項卡**列出已安裝的 ODBC 驅動程式。  
  
-   **追蹤選項卡**使您能夠指定 ODBC 驅動程式管理員追蹤對 ODBC 的呼叫功能。 您可以為每個已安裝的 ODBC 應用程式單獨配置追蹤。  
  
-   **連線池選項卡**使您能夠為每個已安裝的驅動程式選擇連接選項。  
  
-   **關於選項卡**列出已安裝的 ODBC 元件檔案。  
  
 添加數據源後,可以使用**ODBC 數據來源管理員**對話方塊配置對數據源的訪問。 選擇數據源,然後單擊其中一個選項卡以編輯或查看資訊。
