---
title: 步驟 1:設定 pyodbc Python 開發環境 | Microsoft Docs
ms.custom: ''
ms.date: 07/06/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 74e69704-e63c-450b-9207-5c1491d0e0f5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7dd2063a527d782833f2abfcbd635de30aa27117
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80926781"
---
# <a name="step-1-configure-development-environment-for-pyodbc-python-development"></a>步驟 1:設定 pyodbc Python 開發的開發環境

## <a name="windows"></a>Windows  
在 Windows 上使用 Python - pyodbc 連線到 SQL Database：
  
1. **下載 Python 安裝程式**。  
  如果您的電腦沒有 Python，請加以安裝。 移至 [Python 下載頁面](https://www.python.org/downloads/windows/)並下載適當的安裝程式。 例如，如果您是在 64 位元的電腦上，請下載 Python 2.7 或 3.7 (x64) 安裝程式。  
  
2. **安裝 Python**。  下載安裝程式之後，請執行下列步驟：a. 按兩下檔案以啟動安裝程式。 b. 選取您的語言，並同意條款。 c. 遵循畫面上的指示，並將 Python 安裝在您的電腦上。 d. 若要確認是否已安裝 Python，請前往 `C:\Python27` 或 `C:\Python37` 並執行 `python -V` 或 `py -V` (適用於 3.x) 
      
3. [**安裝 Windows 上的 Microsoft ODBC Driver for SQL Server**](../../odbc/windows/system-requirements-installation-and-driver-files.md#installing-microsoft-odbc-driver-for-sql-server)
  
4. **以系統管理員身分開啟 cmd.exe**     

5. **使用 pip 安裝 pyodbc - Python 套件管理員** (使用已安裝的 Python 路徑取代 `C:\Python27\Scripts`)
```  
> cd C:\Python27\Scripts  
> pip install pyodbc  
```  

  
## <a name="linux"></a>Linux 
使用 Python - pyodbc 連線到 SQL Database：
  
1. **開啟終端機**  

2. [**在 Linux 上安裝 Microsoft ODBC Driver for SQL Server**](../../odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

3.  **安裝 pyodbc**  
```  
> sudo -H pip install pyodbc
```
