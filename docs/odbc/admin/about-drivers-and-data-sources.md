---
title: 關於驅動程式和資料源 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC data source administrator [ODBC], concepts
ms.assetid: 2bb83ef1-4bbe-4be3-8c32-c4d1140aae1d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7dffeea3bea7e3fbfa66e534ecaa758fbc2064d5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307219"
---
# <a name="about-drivers-and-data-sources"></a>關於驅動程式和資料來源
*驅動程式*是處理 ODBC 請求並將數據傳回給應用程式的元件。 如有必要,驅動程式將應用程式的請求修改為數據源可以理解的窗體。 您必須使用驅動程式的安裝程式從電腦添加或刪除驅動程式。  
  
 *數據來源*是驅動程式存取的資料庫或檔,由資料源名稱 (DSN) 標識。 使用 ODBC 資料來源管理員從系統中添加、配置和刪除數據來源。 下表描述了可以使用的數據源類型。  
  
|資料來源|描述|  
|-----------------|-----------------|  
|User|使用者 DSN 是電腦的本地,只能由當前使用者使用。 它們在HKEY_CURRENT_USER註冊表子樹中註冊。|  
|系統|系統 DSN 是電腦的本地,而不是專用於使用者。 系統或任何具有許可權的使用者可以使用使用系統 DSN 設置的數據源。 系統 DSN 在HKEY_LOCAL_MACHINE註冊表子樹中註冊。|  
|檔案|檔 DSN 是基於檔的源,可以在安裝了相同驅動程式的所有用戶之間共用,因此可以訪問資料庫。 這些數據源不需要專用於使用者,也不需要是計算機的本地數據源。 檔數據源名稱不由專用註冊表項標識;相反,它們由具有 .dsn 擴展名的檔名標識。|  
  
 使用者和系統數據源統稱為*計算機*數據源,因為它們是計算機的本地數據來源。  
  
 每個資料來源在**ODBC 資料來源管理員**對話方塊中都有一個選項卡。 如需資料來源的詳細資訊，請參閱 [資料來源](../../odbc/reference/data-sources.md)。
