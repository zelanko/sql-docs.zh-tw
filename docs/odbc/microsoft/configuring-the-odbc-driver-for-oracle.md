---
title: "設定 oracle 的 ODBC 驅動程式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- configuring ODBC driver for Oracle [ODBC]
- ODBC driver for Oracle [ODBC], configuring
ms.assetid: 0a5f827c-0b80-4627-85cb-f10292b9fb33
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 64e6dfe9f31eb983170f08e9fcd3e0705ba9ae62
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="configuring-the-odbc-driver-for-oracle"></a>設定 oracle 的 ODBC 驅動程式
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用由 Oracle 提供的 ODBC 驅動程式。  
  
 您可以控制 for Oracle 的 ODBC 驅動程式的效能，了解資料環境，並正確設定參數的資料來源連接，透過[ODBC 資料來源管理員](../../odbc/admin/odbc-data-source-administrator.md)對話方塊方塊中，或透過連線字串參數。 對話方塊中提供下列控制項連接到資料來源使用對話方塊或使用連接字串：  
  
-   **使用者 DSN 索引標籤**列出本機電腦的資料來源名稱。  
  
-   **系統 DSN 索引標籤**可讓您新增或移除系統資料來源。 系統資料來源可以存取本機電腦上的所有使用者。  
  
-   **檔案 DSN 索引標籤**可讓您新增或移除本機電腦上的檔案資料來源。 檔案資料來源可以共用的所有使用者都有相同的驅動程式安裝。  
  
-   **驅動程式 索引標籤**會列出已安裝的 ODBC 驅動程式。  
  
-   **追蹤索引標籤**可讓您指定 ODBC 驅動程式管理員的 ODBC 函數呼叫的追蹤方式。 您可以設定個別追蹤每個已安裝的 ODBC 應用程式。  
  
-   **連線共用 索引標籤**可讓您選取每個已安裝的驅動程式的連接選項。  
  
-   **有關 索引標籤**列出已安裝的 ODBC 元件檔案。  
  
 加入資料來源之後，您可以使用**ODBC 資料來源管理員**對話方塊來設定您的資料來源的存取。 選取資料來源，然後按一下其中一個索引標籤，以編輯或檢視的資訊。

