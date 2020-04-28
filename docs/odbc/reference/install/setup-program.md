---
title: 安裝程式 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81296148"
---
# <a name="setup-program"></a>安裝程式
> **注意：** 從 Windows XP 和 Windows Server 2003 開始， **ODBC 包含在 windows 作業系統中**。 您只應該在舊版 Windows 上明確安裝 ODBC。  
  
 使用者執行安裝程式以啟動安裝程式。 安裝程式是由應用程式或驅動程式開發人員所撰寫。 除了安裝 ODBC 元件之外，它還可以安裝其他軟體。 例如，應用程式開發人員可能會使用相同的安裝程式來安裝 ODBC 元件，並安裝其應用程式。  
  
 開發人員可以從頭開始撰寫安裝程式，使用 Microsoft® Windows® SDK 安裝公用程式或其他廠商的安裝軟體。 如此一來，這些開發人員就可以完全掌控安裝程式的外觀與風格。 您可以撰寫安裝程式來安裝其他軟體，例如 ODBC 應用程式。 如需 Windows SDK 安裝程式公用程式的詳細資訊，請參閱 Windows SDK 檔。  
  
 安裝程式實際完成多少安裝，取決於它在安裝程式 DLL 中呼叫的功能。 安裝程式 DLL 包含用來安裝個別 ODBC 元件的函式。 安裝程式只會呼叫安裝程式 DLL 中的**SQLInstallDriverManager**、 **SQLInstallDriverEx**或**SQLInstallTranslatorEx** ，以抓取要安裝元件的目錄路徑，並將元件的相關資訊新增至登錄。 這些函數並不會實際複製檔案;安裝程式會使用這些函式之引數中的資訊來執行這項工作。  
  
 安裝程式 DLL 也包含可移除 ODBC 元件的函式。 安裝程式會在安裝程式 DLL 中呼叫**SQLRemoveDriverManager**、 **SQLRemoveDriver**或**SQLRemoveTranslator** ，以遞減元件在登錄中的使用計數，如果元件的新使用量計數降為0，則從登錄中移除元件的所有相關資訊。 這些函數實際上不會移除元件的檔案;如果新的使用計數降到0，則安裝程式會執行此步驟。
