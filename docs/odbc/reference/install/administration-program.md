---
description: 管理程式
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5aef5e00fa69fd1f699228b2c0ac82b2a8041962
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429030"
---
# <a name="administration-program"></a>管理程式
> [!NOTE]  
>  從 Windows XP 和 Windows Server 2003 開始，ODBC 會包含在 Windows 作業系統中。 您應該只在舊版的 Windows 上明確地安裝 ODBC。  
  
 管理程式（ODBC 管理員）隨附于 Windows SDK/MDAC SDK。 這項程式可由 SDK 的使用者轉散發。 此外，開發人員也可以撰寫自己的系統管理程式。 一般而言，開發人員只會在想要保有資料來源設定的完整控制權，或者是直接從做為系統管理程式的應用程式設定資料來源時，才撰寫自己的系統管理程式。 例如，試算表程式可能會允許使用者在執行時間加入並使用資料來源。  
  
 系統管理程式會先載入安裝程式 DLL。 然後，它會呼叫安裝程式 DLL 中的函式，以執行下列工作：  
  
-   **以互動方式加入、修改或刪除資料來源。** 管理程式可以呼叫 **SQLManageDataSources**、 **SQLCreateDataSource**或 **SQLConfigDataSource**。  
  
     **SQLManageDataSources** 會顯示一個對話方塊，讓使用者可以加入、修改或刪除資料來源，以及指定追蹤選項;當直接從主控台叫用安裝程式 DLL 時，會呼叫此函式。 **SQLCreateDataSource** 會顯示一個對話方塊，使用者只能在其中加入資料來源。 **SQLConfigDataSource** 會將呼叫直接傳遞至驅動程式安裝 DLL。  
  
     在所有情況下，安裝程式 DLL 都會在驅動程式安裝程式 DLL 中呼叫 **ConfigDSN** ，以實際加入、修改或刪除資料來源。 驅動程式安裝程式 DLL 可能會提示使用者提供其他資訊。  
  
-   **以無訊息方式加入、修改或刪除資料來源。** 管理程式會呼叫安裝程式 DLL 中的 **SQLConfigDataSource** ，並將它傳遞給它一個 null 視窗控制碼、要新增、修改或刪除的資料來源名稱，以及登錄值的清單。 安裝程式 DLL 會在驅動程式安裝程式 DLL 中呼叫 **ConfigDSN** ，以實際加入、修改或刪除資料來源。  
  
-   **加入、修改或刪除預設資料來源。** 預設資料來源與任何其他資料來源相同，不同之處在于它的名稱是預設值。 新增、修改或刪除它的方式與任何其他資料來源相同。
