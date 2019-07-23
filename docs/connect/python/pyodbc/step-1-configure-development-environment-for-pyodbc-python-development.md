---
title: '步驟 1: 設定 pyodbc Python 開發環境 |Microsoft Docs'
ms.custom: ''
ms.date: 07/06/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 74e69704-e63c-450b-9207-5c1491d0e0f5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a1a43540d866faaf79b1c020eb255689862e6d97
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992517"
---
# <a name="step-1-configure-development-environment-for-pyodbc-python-development"></a>步驟 1︰設定 pyodbc Python 開發的開發環境

## <a name="windows"></a>Windows  
使用 pyodbc on Windows 連接到 SQL Database:
  
1. **下載 Python 安裝程式**。  
  如果您的電腦沒有 Python, 請安裝它。 移至[Python 下載頁面](https://www.python.org/downloads/windows/)並下載適當的安裝程式。 例如, 如果您是在64位的電腦上, 請下載 Python 2.7 或 3.7 (x64) 安裝程式。  
  
2. **安裝 Python**。  下載安裝程式之後, 請執行下列步驟: a。 按兩下檔案以啟動安裝程式。 B. 選取您的語言, 並同意條款。 c. 遵循畫面上的指示, 並將 Python 安裝在您的電腦上。 d. 您可以藉由`C:\Python27`前往或`C:\Python37`來確認 Python 是否已安裝, 並`py -V`執行`python -V`或 (適用于 3.x) 
      
3. [**安裝 Windows 上的 Microsoft ODBC Driver for SQL Server**](../../odbc/windows/system-requirements-installation-and-driver-files.md#installing-microsoft-odbc-driver-for-sql-server)
  
4. **以系統管理員身分開啟 cmd.exe**     

5. **使用 Pip 安裝 pyodbc-Python 套件管理員**(將`C:\Python27\Scripts`取代為您安裝的 Python 路徑)
```  
> cd C:\Python27\Scripts  
> pip install pyodbc  
```  

  
## <a name="linux"></a>Linux 
使用 Python 連接到 SQL Database-pyodbc:
  
1. **開啟終端機**  

2. [**在 Linux 上安裝 Microsoft ODBC Driver for SQL Server**](../../odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

3.  **安裝 pyodbc**  
```  
> sudo -H pip install pyodbc
```
