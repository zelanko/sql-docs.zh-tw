---
title: 系統管理程式 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d8a2a8363371d6f6c3644c2b7b49aa77644d496e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306639"
---
# <a name="administration-program"></a>管理程式
> [!NOTE]  
>  從 Windows XP 和 Windows Server 2003 開始，ODBC 包含在 Windows 作業系統中。 您只應該在舊版 Windows 上明確安裝 ODBC。  
  
 系統管理程式是 ODBC 系統管理員，隨附在 Windows SDK/MDAC SDK 中。 此程式可供 SDK 的使用者轉散發。 此外，開發人員也可以撰寫自己的系統管理程式。 一般而言，開發人員只有在想要保有資料來源設定的完整控制權，或直接從作為管理程式的應用程式設定資料來源時，才會撰寫自己的系統管理程式。 例如，試算表程式可讓使用者在執行時間新增和使用資料來源。  
  
 系統管理程式會先載入安裝程式 DLL。 然後，它會呼叫安裝程式 DLL 中的函式來執行下列工作：  
  
-   **以互動方式加入、修改或刪除資料來源。** 系統管理程式可以呼叫**SQLManageDataSources**、 **SQLCreateDataSource**或**SQLConfigDataSource**。  
  
     **SQLManageDataSources**會顯示一個對話方塊，使用者可以在其中新增、修改或刪除資料來源，並指定追蹤選項;從 [控制台] 直接叫用安裝程式 DLL 時，會呼叫這個函式。 **SQLCreateDataSource**會顯示一個對話方塊，使用者只能在其中新增資料來源。 **SQLConfigDataSource**會將呼叫直接傳遞到驅動程式安裝 DLL。  
  
     在所有情況下，安裝程式 DLL 都會呼叫驅動程式安裝 DLL 中的**ConfigDSN** ，以實際新增、修改或刪除資料來源。 驅動程式安裝 DLL 可能會提示使用者提供其他資訊。  
  
-   **以無訊息方式新增、修改或刪除資料來源。** 管理程式會在安裝程式 DLL 中呼叫**SQLConfigDataSource** ，並將它傳遞給它一個 null 視窗控制碼、要加入、修改或刪除的資料來源名稱，以及登錄的值清單。 安裝程式 DLL 會呼叫驅動程式安裝 DLL 中的**ConfigDSN** ，以實際新增、修改或刪除資料來源。  
  
-   **加入、修改或刪除預設資料來源。** 預設資料來源與其他任何資料來源相同，不同之處在于它的名稱是預設值。 其加入、修改或刪除的方式與任何其他資料來源相同。
