---
title: 部署 JDBC 驅動程式
ms.custom: ''
ms.date: 03/13/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3ad3508d-d9b1-47fb-a63b-21cdc3ed44e0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 36eb8896a18a6dd87e9b75818f6e4aae2c336905
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922435"
---
# <a name="deploying-the-jdbc-driver"></a>部署 JDBC 驅動程式

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

當部署會相依於 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 的應用程式時，必須隨著應用程式一起轉散發 JDBC 驅動程式。 不同於 Windows Data Access Components (Windows DAC) (它是 Windows 作業系統的元件)，JDBC 驅動程式被視為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的元件。  
  
有兩種方法可利用應用程式部署 JDBC Driver。 第一種方法就是將 JDBC 驅動程式檔案包括為自訂安裝封裝的一部份。 第二種方法涉及使用 Microsoft 提供的 JDBC 安裝套件，其可從 [Microsoft JDBC Driver for SQL Server 下載頁面](download-microsoft-jdbc-driver-for-sql-server.md)下載。  
  
下列幾節討論如何在 Windows 及 UNIX 作業系統上使用 JDBC 安裝封裝。  
  
> [!NOTE]  
> 如需一般部署 Java 應用程式的相關資訊，請參閱 Java 網站。  
  
## <a name="deploying-the-jdbc-driver-on-windows-systems"></a>在 Windows 系統上部署 JDBC 驅動程式

在 Windows 作業系統上部署 JDBC 驅動程式時，您必須將通常名為 `sqljdbc_<version>_<language>.zip` 的 ZIP 壓縮安裝套件解壓縮。

## <a name="deploying-the-driver-on-unix-systems"></a>在 UNIX 系統上部署驅動程式

在 UNIX 作業系統上部署 JDBC 驅動程式時，您必須使用安裝套件的 GZIP 檔版本，通常名為 `sqljdbc_<version>_<language>.tar.gz`。  
  
在安裝 JDBC 驅動程式之前，請確定 gzip 和 tar 公用程式已安裝在使用者的系統上，並確定包含這兩個公用程式之執行檔的資料夾已新增至 PATH 環境變數。  
  
若要將壓縮的 tar 檔案解壓縮，請導覽至您要解壓縮驅動程式的目錄，並輸入下列命令：  
  
`gzip -d sqljdbc_<version>_<language>.tar.gz`  
  
若要將 tar 檔案解壓縮，請將它移到您要安裝驅動程式的目錄，並輸入下列命令：  
  
`tar -xf sqljdbc_<version>_<language>.tar`  

## <a name="legalities-of-driver-redistribution"></a>轉散發驅動程式的合法性

JDBC Driver 6.0、6.2、6.4、7.0、7.2、7.4 與 8.2 版均為可轉散發。 檢閱授權合約中的「可轉散發程式碼」  條款。

JDBC 驅動程式 4.x 版已過時且已淘汰。 對 4.x 的支援已於 2018 年之前過期。

## <a name="see-also"></a>另請參閱

[JDBC 驅動程式概觀](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
