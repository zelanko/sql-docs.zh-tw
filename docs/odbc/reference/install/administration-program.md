---
title: 管理程式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- administration program [ODBC]
- ODBC administrator [ODBC]
ms.assetid: a6c8248a-7a01-42e7-aaed-99dc94d50028
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6f7b3f0420fa7f0ed2226201d06a339341f5f734
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="administration-program"></a>管理程式
> [!NOTE]  
>  從 Windows XP 和 Windows Server 2003，ODBC 隨附於 Windows 作業系統。 您只明確應該在舊版 Windows 上安裝 ODBC。  
  
 管理程式，而 ODBC 管理員，隨附於 Windows SDK/MDAC SDK。 此程式和使用者的 sdk 可轉散發。 此外，開發人員可以撰寫自己的管理程式。 一般而言，開發人員撰寫自己的管理程式，只有當他們想保留的資料來源設定，擁有完整控制權，或它們要設定的應用程式，做為管理程式直接從資料來源。 例如，試算表程式可能會允許使用者新增，然後在執行階段中使用資料來源。  
  
 管理程式第一次載入安裝程式 DLL。 然後，它會呼叫函式在安裝程式中的 DLL，以便執行下列工作：  
  
-   **新增、 修改或刪除資料來源，以互動方式。** 管理程式可以呼叫**SQLManageDataSources**， **SQLCreateDataSource**，或**SQLConfigDataSource**。  
  
     **SQLManageDataSources**顯示的對話方塊的使用者可以新增、 修改或刪除資料來源和指定的追蹤選項，直接從控制項面板叫用安裝程式的 DLL 時，會呼叫此函數。 **SQLCreateDataSource**顯示的對話方塊，使用者可以只將資料來源。 **SQLConfigDataSource**會傳遞至驅動程式安裝 DLL 的直接呼叫。  
  
     在所有情況下，安裝程式的 DLL 呼叫**ConfigDSN**中的驅動程式安裝 DLL 實際加入、 修改或刪除資料來源。 驅動程式安裝 DLL 可能會提示使用者輸入其他資訊。  
  
-   **新增、 修改或刪除資料來源以無訊息模式。** 系統管理程式呼叫**SQLConfigDataSource**中的安裝程式 DLL 和傳遞它 null 視窗處理，來新增、 修改或刪除資料來源的名稱和登錄值的清單。 安裝程式的 DLL 呼叫**ConfigDSN**中的驅動程式安裝 DLL 實際加入、 修改或刪除資料來源。  
  
-   **新增、 修改或刪除預設資料來源。** 預設的資料來源不同之處在於其名稱是預設值是與其他資料來源相同。 已加入、 修改或刪除以相同的方式與任何其他資料來源。
