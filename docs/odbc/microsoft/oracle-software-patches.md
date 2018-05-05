---
title: Oracle 軟體修補程式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], Oraclesoftware patches
- Oracle software patches [ODBC]
ms.assetid: 1275157b-f4e1-4c24-b273-c02555e261c2
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 773b7f179d70a4ba04b5516f930c4e1a39a31963
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="oracle-software-patches"></a>Oracle 軟體修補程式
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 相反地，使用由 Oracle 提供的 ODBC 驅動程式。  
  
 Oracle 伺服器產品，其用戶端元件的修補程式所需的正常運作的數個 Microsoft 產品和技術，包括 Microsoft ODBC Driver for Oracle，Microsoft OLE DB Provider for Oracle，網際網路資訊服務 (IIS)、 元件服務 （或 Microsoft Transaction Server，如果您使用 Windows NT），依此類推。  
  
> [!NOTE]  
>  下列指示可能無法完全精確，因為 Oracle FTP 站台可能有所變更。  
  
### <a name="to-download-the-oracle-software-patches"></a>若要下載的 Oracle 軟體修補程式  
  
1.  連接到 oracle ftp.oracle.com 在公用的 FTP 站台。為 「 匿名 」 的使用者識別碼和密碼是您的電子郵件地址。  
  
2.  瀏覽至下列目錄： /server/wgt_tech/server/windowsNT。  
  
3.  若要下載 Windows 95、 Windows 98 和 NT/Windows 2000年最相關的修補程式，瀏覽至您的 Oracle 版本子目錄 — 7.3 或 8.0。 兩個子目錄是 /73patchsets 和 /80patchsets。  
  
4.  若要下載修補程式 Oracle 的網路技術，可能是 SQL * Net 或 Net8，瀏覽至下列目錄: / 網路。  
  
 從您網頁瀏覽器存取此 FTP 站台可能無法運作。 如果您遇到問題，請嘗試使用 「 傳統 」 的 FTP 用戶端，或使用 DOS 命令提示字元。  
  
> [!NOTE]  
>  因為 Oracle 在目前版本中修正的 bug，然後將它們 retrofits 至較早的版本使用軟體修補程式，建議您下載最新的修補程式。 這特別適用於 Oracle 伺服器的用戶端元件。 如果您有安裝這些修補程式的相關問題，請連絡 Oracle 支援。
