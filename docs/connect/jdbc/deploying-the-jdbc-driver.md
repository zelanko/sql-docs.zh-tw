---
title: 部署 JDBC 驅動程式 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3ad3508d-d9b1-47fb-a63b-21cdc3ed44e0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3e7898f66631fd9ca9d75573d5025bb732db8208
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67956720"
---
# <a name="deploying-the-jdbc-driver"></a>部署 JDBC 驅動程式
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  當部署會相依於 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 的應用程式時，必須隨著應用程式一起轉散發 JDBC 驅動程式。 不同於 Windows Data Access Components (Windows DAC) (它是 Windows 作業系統的元件)，JDBC 驅動程式被視為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的元件。  
  
 有兩種方法可利用應用程式部署 JDBC Driver。 第一種方法就是將 JDBC 驅動程式檔案包括為自訂安裝封裝的一部份。 第二種方法牽涉到使用 Microsoft 提供的 JDBC 安裝套件，您可以從 [Microsoft JDBC Driver for SQL Server 開發人員中心](https://go.microsoft.com/fwlink/?LinkId=70166)下載此套件。  
  
 下列幾節討論如何在 Windows 及 UNIX 作業系統上使用 JDBC 安裝封裝。  
  
> [!NOTE]  
>  如需一般部署 Java 應用程式的相關資訊，請參閱 Java 網站。  
  
## <a name="deploying-the-jdbc-driver-on-windows-systems"></a>在 Windows 系統上部署 JDBC 驅動程式  
 在 Windows 作業系統上部署 JDBC 驅動程式時，您必須使用安裝套件的可執行 ZIP 檔版本，通常名為 `sqljdbc_<version>_<language>.exe`。  
  
 若要無訊息地執行可執行的 ZIP 檔，必須在命令列上或批次檔中使用 `/auto` 命令列選項，如下所示：  
  
 `sqljdbc_<version>_<language>.exe /auto`  
  
> [!NOTE]  
>  使用 `/auto` 選項時，它並不是真的無訊息安裝，因為 WinZip 對話方塊仍會出現在使用者的畫面上。 不過，您將不需要與其互動，而且解壓縮作業一完成，它就會關閉。  
  
## <a name="deploying-the-driver-on-unix-systems"></a>在 UNIX 系統上部署驅動程式  
 在 UNIX 作業系統上部署 JDBC 驅動程式時，您必須使用安裝套件的 GZIP 檔版本，通常名為 `sqljdbc_<version>_<language>.tar.gz`。  
  
 在安裝 JDBC 驅動程式之前，請確定 gzip 和 tar 公用程式已安裝在使用者的系統上，並確定包含這兩個公用程式之執行檔的資料夾已新增至 PATH 環境變數。  
  
 若要將壓縮的 tar 檔案解壓縮，請導覽至您要解壓縮驅動程式的目錄，並輸入下列命令：  
  
 `gzip -d sqljdbc_<version>_<language>.tar.gz`  
  
 若要將 tar 檔案解壓縮，請將它移到您要安裝驅動程式的目錄，並輸入下列命令：  
  
 `tar -xf sqljdbc_<version>_<language>.tar`  
  
## <a name="see-also"></a>另請參閱  
 [JDBC Driver 概觀](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  
