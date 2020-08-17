---
description: Oracle 軟體修補程式
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e6bc07ae904b8bb682d9a5cf9eefebe00dc532aa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340684"
---
# <a name="oracle-software-patches"></a>Oracle 軟體修補程式
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 請改用 Oracle 提供的 ODBC 驅動程式。  
  
 許多 Microsoft 產品和技術都必須有修補程式才能正常運作，包括 Microsoft ODBC Driver for Oracle、Microsoft OLE DB Provider for Oracle、Internet Information Services (IIS) 、Component Services (或 Microsoft Transaction Server （如果您使用 Windows NT) 等）。  
  
> [!NOTE]  
>  下列指示可能無法完全精確，因為 Oracle FTP 網站有可能變更。  
  
### <a name="to-download-the-oracle-software-patches"></a>下載 Oracle 軟體修補程式  
  
1.  連接到公用 FTP 網站，網址為 oracle-ftp.oracle.com。 使用者識別碼是「匿名」，而密碼是您的電子郵件地址。  
  
2.  流覽至下列目錄：/server/wgt_tech/server/windowsNT。  
  
3.  若要下載與 Windows 95、Windows 98 和 Windows NT/Windows 2000 最相關的修補程式，請流覽至您的 Oracle-7.3 或8.0 版本的子目錄。 這兩個子目錄為/73patchsets 和/80patchsets。  
  
4.  若要下載 Oracle 網路技術（SQL * Net 或 Net8）的修補程式，請流覽至下列目錄：/network。  
  
 從網頁瀏覽器存取這個 FTP 網站可能無法運作。 如果您遇到問題，請嘗試使用「傳統」 FTP 用戶端，或使用 DOS 命令提示字元。  
  
> [!NOTE]  
>  由於 Oracle 會修正目前版本中的 bug，然後使用軟體修補程式將它們 retrofits 到較早的版本，因此建議您下載可用的最新修補程式。 尤其是對於 Oracle 伺服器用戶端元件而言也是如此。 如果您有關于安裝這些修補程式的問題，請洽詢 Oracle 支援。
