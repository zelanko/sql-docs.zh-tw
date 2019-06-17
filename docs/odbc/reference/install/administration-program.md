---
title: 管理程式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- administration program [ODBC]
- ODBC administrator [ODBC]
ms.assetid: a6c8248a-7a01-42e7-aaed-99dc94d50028
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 740a09d9a6bceb9d3f290faa71444df0d1e7c6c7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62629558"
---
# <a name="administration-program"></a>管理程式
> [!NOTE]  
>  從 Windows XP 和 Windows Server 2003 開始，ODBC 會包含在 Windows 作業系統。 您只明確應該安裝在舊版 Windows 上的 ODBC。  
  
 隨附於 Windows SDK/MDAC SDK 管理計劃時，ODBC 系統管理員。 此程式和可轉散發的 sdk 的使用者。 此外，開發人員可以撰寫自己的管理程式。 一般而言，開發人員撰寫自己的管理程式，只有當他們想保留完全控制的資料來源設定，或如果他們要設定直接從應用程式做為管理程式的資料來源。 例如，試算表程式可能會允許使用者新增，然後在執行階段中使用資料來源。  
  
 管理程式第一次載入安裝程式 DLL。 然後，它會呼叫函式在安裝程式 DLL，以執行下列工作：  
  
-   **新增、 修改或刪除資料來源，以互動方式。** 管理程式可以呼叫**SQLManageDataSources**， **SQLCreateDataSource**，或**SQLConfigDataSource**。  
  
     **SQLManageDataSources**會顯示一個對話方塊，使用者可以新增、 修改或刪除資料來源和指定的追蹤選項，從控制台直接叫用安裝程式 DLL 時，會呼叫此函數。 **SQLCreateDataSource**顯示的對話方塊，使用者只能新增資料來源。 **SQLConfigDataSource**會傳遞至驅動程式安裝程式 DLL 的直接呼叫。  
  
     在所有情況下，安裝程式 DLL 會呼叫**ConfigDSN**的驅動程式安裝 DLL 以實際加入、 修改或刪除資料來源。 驅動程式安裝 DLL 可能會提示使用者輸入其他資訊。  
  
-   **新增、 修改或刪除資料來源以無訊息模式。** 管理程式呼叫**SQLConfigDataSource**在安裝程式 DLL 並傳遞它 null 視窗處理，要新增、 修改或刪除的資料來源的名稱和登錄值的清單。 安裝程式 DLL 會呼叫**ConfigDSN**的驅動程式安裝 DLL 以實際加入、 修改或刪除資料來源。  
  
-   **新增、 修改或刪除預設資料來源。** 預設的資料來源等同於任何其他資料來源，不同之處在於其名稱是預設值。 它會新增、 修改或刪除相同的方式，為任何其他資料來源。
