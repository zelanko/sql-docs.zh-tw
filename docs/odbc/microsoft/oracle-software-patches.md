---
title: Oracle 軟體修補程式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], Oraclesoftware patches
- Oracle software patches [ODBC]
ms.assetid: 1275157b-f4e1-4c24-b273-c02555e261c2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fce38aabddfc3891314940d4b7cb21f02965c083
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68100771"
---
# <a name="oracle-software-patches"></a>Oracle 軟體修補程式
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 所提供的 ODBC 驅動程式。  
  
 需要 Oracle 伺服器產品及其用戶端元件的修補程式，才能正常運作數種 Microsoft 產品和技術，包括 Microsoft ODBC Driver for Oracle、Microsoft OLE DB Provider for Oracle、Internet Information服務（IIS）、元件服務（或 Microsoft 交易伺服器，如果您使用的是 Windows NT）等等。  
  
> [!NOTE]  
>  下列指示可能不完全精確，因為 Oracle FTP 網站可能會有所變更。  
  
### <a name="to-download-the-oracle-software-patches"></a>下載 Oracle 軟體修補程式  
  
1.  連接到公用 FTP 網站，網址為 oracle-ftp.oracle.com。 使用者識別碼是「匿名」，而密碼則是您的電子郵件地址。  
  
2.  流覽至下列目錄：/server/wgt_tech/server/windowsNT。  
  
3.  若要下載與 Windows 95、Windows 98 和 Windows NT/Windows 2000 相關的修補程式，請流覽至您的 Oracle 版本的子目錄-7.3 或8.0。 這兩個子目錄是/73patchsets 和/80patchsets。  
  
4.  若要下載 Oracle 網路技術（SQL * Net 或 Net8）的修補程式，請流覽至下列目錄：/network。  
  
 從您的網頁瀏覽器存取此 FTP 網站可能無法正常執行。 如果您遇到問題，請嘗試使用「傳統」 FTP 用戶端，或使用 DOS 命令提示字元。  
  
> [!NOTE]  
>  因為 Oracle 會修正目前版本中的 bug，然後使用軟體修補程式將其 retrofits 到舊版，建議您下載可用的最新修補程式。 這對於 Oracle 伺服器用戶端元件而言更是如此。 如果您有關于安裝這些修補程式的問題，請洽詢 Oracle 支援。
