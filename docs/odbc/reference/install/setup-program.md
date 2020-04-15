---
title: 安裝程式 |微軟文件
ms.custom: ''
ms.date: 08/31/2016
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC], setup program
ms.assetid: 9cc5d75d-b293-41e5-927c-10f4af2e7af1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b89cae70db65bd2aa54b8e9789a5c2b35696923e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296148"
---
# <a name="setup-program"></a>安裝程式
> **註:** 從 Windows XP 和 Windows 伺服器 2003 開始 **,ODBC 包含在 Windows 作業系統中**。 您只應在早期版本的 Windows 上顯式安裝 ODBC。  
  
 使用者運行安裝程式以啟動安裝過程。 安裝程式由應用程式或驅動程式開發人員編寫。 除了安裝 ODBC 元件外,還可以安裝其他軟體。 例如,應用程式開發人員可能使用相同的安裝程式來安裝 ODBC 元件並安裝其應用程式。  
  
 開發人員可以使用 Microsoft ® Windows ® SDK 設置實用程式或來自其他供應商的設置軟體,從頭開始編寫安裝程式。 這使得這些開發人員能夠完全控制安裝程序的外觀。 可以編寫安裝程式來安裝其他軟體,如ODBC應用程式。 有關 Windows SDK 設定實用程式的詳細資訊,請參閱 Windows SDK 文檔。  
  
 安裝程式實際完成安裝量取決於安裝程式 DLL 中調用的功能。 安裝程式 DLL 包含安裝單個 ODBC 元件的功能。 安裝程式只需在安裝程式 DLL 中呼叫**SQLInstallDriverManager、SQLInstallDriverEx**或**SQLInstallTranslatorEx,** 即可檢索要在其中安裝元件的目錄的路徑,並將有關元件的資訊添加**SQLInstallDriverEx**到註冊表中。 這些函數實際上不複製檔;因此,這些函數不會複製檔。安裝程式使用這些函數參數中的資訊來這樣做。  
  
 安裝程式 DLL 還包含移除 ODBC 元件的功能。 安裝程式在安裝程式 DLL 中呼叫**SQLRemoveDriverManager、SQLRemoveDriver**或**SQLRemove 轉換器**,以在註冊表中減少元件的使用計數,如果元件的新使用計數降至 0,則從註冊表中刪除有關**SQLRemoveDriver**該元件的所有資訊。 這些函數實際上不會刪除元件的檔,而是刪除元件的檔。如果新的使用計數下降到 0,安裝程式將執行此項。
