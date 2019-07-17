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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dc79bb5d12b53938e3e2ef1c531fd03b0002ed78
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093827"
---
# <a name="setup-program"></a>安裝程式
> **注意：** 從 Windows XP 和 Windows Server 2003、windows **ODBC 會包含在 Windows 作業系統中**。 您只明確應該安裝在舊版 Windows 上的 ODBC。  
  
 使用者執行安裝程式，以啟動安裝程序。 安裝程式會寫入應用程式或驅動程式開發人員。 除了安裝 ODBC 元件，它可以安裝其他軟體。 例如，應用程式開發人員可能會使用相同的安裝程式來安裝 ODBC 元件並安裝他們的應用程式。  
  
 開發人員可以從頭開始撰寫安裝程式，使用 Microsoft® Windows® SDK 安裝程式公用程式或來自其他廠商的安裝程式軟體。 這可讓開發人員安裝程式的外觀與風格的完整控制。 安裝程式可以撰寫程式來安裝其他軟體，例如 ODBC 應用程式。 如需有關 Windows SDK 安裝程式公用程式的詳細資訊，請參閱 Windows SDK 文件。  
  
 在安裝中有多少工作實際上是由安裝程式，取決於哪些函數它在安裝程式 DLL 的呼叫。 安裝程式 DLL 包含安裝個別的 ODBC 元件的函式。 安裝程式只會呼叫**SQLInstallDriverManager**， **SQLInstallDriverEx**，或**SQLInstallTranslatorEx**在安裝程式 DLL 來擷取的路徑元件是安裝，並將元件的相關資訊新增至登錄的目錄。 這些函式不實際將複製的檔案;安裝程式會使用這些函式的引數中的資訊。  
  
 安裝程式 DLL 也包含函式來移除 ODBC 元件。 安裝程式呼叫**SQLRemoveDriverManager**， **SQLRemoveDriver**，或**SQLRemoveTranslator**在安裝程式 DLL 來遞減元件的使用方式中的計數登錄和元件的新使用計數降至 0，如果從登錄中移除所有元件的相關資訊。 這些函式不會移除元件的檔案安裝程式會如果新的使用方式計數降至 0。
